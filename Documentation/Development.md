# Replicating the Environment (Docker)

This is the recommended replication method; however, if you really hate Docker, 
consult the instructions for [replicating manually](#replicating-the-environment-manual).

## Replication Instructions

### Install Docker Compose

#### Linux Install

- Most Linux distributions have a package for Docker Compose and you should consult
your distributions documentation for installing it.
  - On Arch, install `docker-compose` with pacman.
- You should ensure your user is added to the `docker` group so you can run without sudo.
  - If you do not want to log out, run `su <your username>` before executing
  Docker commands
- On systemd machines, you should ensure the Docker daemon is started before
executing commands.
  - Start it manually or implement one of the two options given 
  [here](https://wiki.archlinux.org/title/Docker#Installation).

### Create `custom_settings.py`

1. Create a file called `custom_settings.py` in 
`Commitment_to_Change_App/Commitment_to_Change_App/`, next to `settings.py`.
- **Do _NOT_ commit this file under any circumstances!** We do not want to 
  know your database or secret key details, which is why it has been separated 
  from `settings.py`!


2. Paste the following into `custom_settings.py`:
```
# Database
# https://docs.djangoproject.com/en/4.2/ref/settings/#databases
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'postgres',
        'USER': 'postgres',
        'PASSWORD': 'Insecure7',
        'HOST': 'cme-ctc-db',
        'PORT': '5432',
    }
}

# SECURITY WARNING: keep the secret key used in production secret!
SECRET_KEY = ''
```

3. Run the following code in your terminal to generate a secret key:
```
python -c "import secrets; print(secrets.token_urlsafe())"
```

4. Paste the secret key in Step 3 in between single quotes after `SECRET_KEY` 
in `custom_settings.py`.

### Build the Docker Containers

1. Run `docker-compose build`.
2. Verify the containers run with `docker-compose up`.
  - On your host machine, navigate to `127.0.0.1:8000`.
  - You may need to run this twice because the database can be slow to 
  initialize the first time.

### Perform Migrations

1. Run the following commands:
```
docker-compose run cme-ctc-web touch /app/cme_accounts/migrations/__init__.py
docker-compose run cme-ctc-web touch /app/commitments/migrations/__init__.py
docker-compose run cme-ctc-web python manage.py makemigrations
docker-compose run cme-ctc-web python manage.py migrate
```
  - The call to `docker-compose` might be different on Windows. However,
  everything from `run cme-ctc-web` and after should not change.

### Verify the App

You should perform all of the tests specified 
[here](#testing-the-environment-and-app-with-docker).

## Docker-Specific Considerations

Since under Docker replication the database is in a container, all operations
involving it should generally be done in the Docker containers unless there
is an extremely compelling reason not to. This means that migrations and 
test runs should be done in the container. It can be particularly annoying
to frequently type things like 
`docker-compose run cme-ctc-web python manage.py test`, so automation via 
shortening scripts is strongly recommended. See the section below for how
to do so is strongly recommended.


### Migrating in Docker

Since migrations are not currently version controlled, it is best to generate
them within the container so they can be easily discarded with the database if
need be. The `docker-compose` configuration we have manages this by mounting 
volumes for every `*/migrations/` directory. 
However, the volumes mounted at the migration folders  do not initially 
contain `__init__.py`, which will cause the migration process to fail. Since
such files will serve their purpose even when empty, you can `touch` them
from inside the container every time you create/recreate the containers. If you 
are prone to forgetting to do this, it is recommended that you automate this 
process for your migration scripts.

Note that the `touch` calls will cause a restart of the server because files 
have changed. Don't put them on scripts that don't need them (ie non-migration 
scripts).

### General Script Tips

**Convenience scripts should generally be put in `dev_scripts` so they are 
not tracked.**

- You can use `docker-compose exec <command>` instead of 
`docker-compose run <command>` to running in a container that is already up in 
another terminal.
- If you want an interative terminal (for example, with `psql`) you must use
`docker-compose exec -it <command>` or else the script will just execute without
any further input from you.

### Scripts (Linux)

Here are some possible scripts you can make to avoid lots of typing:
- Create the `*/migrations/__init__.py` files:
```
docker-compose run cme-ctc-web touch /app/cme_accounts/migrations/__init__.py
docker-compose run cme-ctc-web touch /app/commitments/migrations/__init__.py
```

- Make migrations while being sure to touch `*/migrations/__init__.py` files:
```
docker-compose run cme-ctc-web touch /app/cme_accounts/migrations/__init__.py
docker-compose run cme-ctc-web touch /app/commitments/migrations/__init__.py
docker-compose run cme-ctc-web python manage.py makemigrations
```
  - You do not need this and the script above, this one is here just in case
  you tend to forget to run the above script.

- Migrate:
```
docker-compose run cme-ctc-web python manage.py migrate
```

- Run general commands from `manage.py` in the container:
```
docker-compose run cme-ctc-web python manage.py "$@"
```
  - *NEVER* use this to run the server, `docker-compose up` already does that for you.
  - If this script had relative path `developer_scripts/manage`, you would call 
  it like `developer_scripts/manage test` to run tests, or `developer_scripts/manage makemigrations cme_accounts` 

# Testing the environment and app (with Docker)

Currently, our unit and integration testing is quite poor. You should both run
the automated tests and perform a manual full-stack test of all features.

## Run the Automated Tests (Docker)

- If the containers are not up, run 
`docker-compose run cme-ctc-web python manage.py test`
- Otherwise you could instead run
`docker-compose exec cme-ctc-web python manage.py test`
in another terminal.

## Full-stack Testing (Docker)

Run `docker-compose up` if your containers are not up and perform the feature 
checks below.

### Feature Checks

1. Create and log in to a new provider account.
2. Create a new course and verify it shows in the dashboard.
3. Edit that course and verify that the changes are reflected.
4. Copy the invite link for that course.
5. Log out.
6. Create and log in to a new clinician account.
7. Use the invite link and verify the course shows in your dashboard.
8. Create a new commitment and verify it shows in the dashboard.
9. Edit that commitment and verify that it changes correctly.
10. Edit the commitment to be associated with a course. Verify it shows in the
course page and status count table.
11. Mark it complete, reopen, mark it discontinued, reopen. Verify that it
shows in the correct sections and that the course view status count table
shows it correctly eac time.
12. Delete the commitment and verify that it is no longer present in the
dashboard or course page.
13. Create another commitment.
14. Using `docker-compose exec -it cme-ctc-db psql -U postgres postgres` in 
another terminal, run the following `psql` command:
```
UPDATE commitments_commitment SET deadline='2000-01-01' WHERE id=2;
```
  - The id should be 2 if you have created no other commitments.
15. Verify that the commitment shows in the expired category on the dashboard
after refreshing.
16. Discontinue the commitment and reopen. Verify that it correctly returns
to the expired category.
17. If all of the above proceed without incident, the software likely functions
correctly.


# Replicating the Environment (Manual)

This method is trickier than [Replicating with Docker](#replicating-the-environment-docker) and is considered deprecated.

## Environment Overview

## Replication Instructions

If you already have Python installed, review the installation to verify that your version of Python is compatible with Django. Afterward, [click here to skip ahead](#install-and-setup-virtual-environment).

---

### Install Python

1. Download Python

   - If you are using a Linux distro with a package manager, consider installing
the latest version of Python from it, as this will likely be better documented
for troubleshooting. In this case, skip steps 1 and 2 once you have done so.
   - Python is not included by default in Windows or Mac, so it must be downloaded and installed from: https://www.python.org/downloads/
   - To check if you have Python installed, type `python --version` into a Command Prompt. If Python is installed correctly, this command should return the currently installed Python version.
   - Download the latest Python version that is supported by Django. We are currently using Django version 4.2, so Python version 3.11.6 is the latest supported version.
     - You can check Python/Django version compatibility here: https://www.python.org/downloads/

2. Install Python

   - In the installation dialogue, make sure to check "Add python.exe to PATH". This allows us to execute Python in the command line by simply typing "python" or "py" instead of navigating to it's install location.![python install](<../Auxiliary Files/Images/Development_Images/Python_addToPath.png>)
     If you forget to check this, you can manually add to PATH later,
     [similarly to how we will do it with PSQL](#install-and-configure-postgresql)
   - Click "install now"
   - Ignore the "Disable path length limit" option shown at the end of installation.

3. Verify Python installation

   - Use `python --version` to verify installation.
   - The Python installer includes the Python package manager, known as pip. You can check if pip is installed and list installed packages by using the following command: `pip list`

---

### Install and setup virtual environment

1. Install venv

   - In your Command Prompt, navigate to whatever directory you want to create your project folder in. The command we are about to run will create a new folder that will hold our virtual environment, as well as our project files once we clone them later.
   - Once in your empty project directory, type `py -m venv venv_name`
     - For example, if you want your virtual environment directory to be named "CME_Project", use the command `py -m venv CME_Project`

2. Ensure venv creation was successful

   - Navigate to your new directory using File Explorer, or use the command line:
     - Type `dir` to check if the directory was successfully created.
     - Type `cd directory_name` to move into your new directory, and then `dir` again to view the directory contents.
   - You should see 3 folders, `Include`, `Lib`, and `Scripts`, as well as a `pyvenv.py` file. ![venv folder](<../Auxiliary Files/Images/Development_Images/checkvenvCreatedSucceessfully.png>)
     - On Linux, the folders will normally be `bin`, `include`, and `lib`.

3. Activate your virtual environment.

- #### IMPORTANT:

  - You will need to activate your virtual environment BEFORE you run the project, EVERY TIME you run the project.
  - While in your new project root directory, type `Scripts\Activate.bat`
    - On Linux, you may instead need to type `source bin/activate` while in
    the directory that is parent to `bin`. This will be omitted from future
    steps.
  - You should now see something like `(Project_name)` before your project path in the command line. This means you are now in your active virtual environment.

    ![venv activated](<../Auxiliary Files/Images/Development_Images/ActivateBat.png>)

---

### Install Django

1. Install the latest version of Django

   - This may be done via Pip or (on some Linux distributions) a package installation. Pip is generally preferred due to venv. However, if you choose to install
system-wide with a package, skip to Step 2.
   - To install with pip, [while still in your active virtual environment](#important), type `pip install django`

2. Create a test project using `django-admin startproject testproject`

   - This MUST be done in the directory you intend to clone the project into.

3. Change into the `testproject` directory
4. Run the Django server with `python manage.py runserver`
5. Connect to `localhost:8000` to verify that Django is running
6. Shut down the server by typing `CTRL + C`
7. Recursively remove the `testproject` directory

---

### Clone the Main Code Repo

1. Navigate to the directory you want the root of the project to live in. All
   future paths will be relative to this directory.
   - NOTE: This must be inside the virtual environment directory [you created earlier](#install-and-setup-virtual-environment).
2. Run
   `git clone https://github.com/lee-blake/Commitment-to-Change-App.git`
   in the desired directory to clone to.

   - Your root folder/venv folder structure should now look similar to this:![Root directory](<../Auxiliary Files/Images/Development_Images/FinalRootFolderStructure.png>)

---

### Install and Configure PostgreSQL

1. Install the latest version of PostgreSQL

   - On many Linux distributions, this may be done via a package. This is the
     preferred method if available because troubleshooting will likely be better
     documented.

   - On Windows and Mac, use the latest installer from: https://www.enterprisedb.com/downloads/postgres-postgresql-downloads
     - On the "Select Components" screen, uncheck "Stack Builder". If you forget this step, just exit out of the Stack Builder Wizard after installation.
     - In the installer, you will be prompted to create a password for the database superuser. You will need this any time you want to access your PostgreSQL databases, so write it down.

**_NOTE:_** If using the PostgreSQL installer on Windows or Mac, skip to step 4. Steps 2 and 3 are performed automatically in the installer.

2. Initialize the database cluster if needed (Linux only)

   - On most Linux installs, a `postgres` user is created and this user must
     be the one to execute the initialization using either `sudo -u postgres initdb --locale en_US.UTF-8 -E UTF8 -D '/var/lib/postgres/data'` or using `su` to switch to `postgres` before running `initdb --locale en_US.UTF-8 -E UTF8 -D '/var/lib/postgres/data'`

3. Start the PostgreSQL service if needed (Linux only)

   - On `systemd` Linux systems, use `sudo systemctl start postgresql`. You may also want to run `sudo systemctl enable postgresql` if you do not want to run the start command every time.

4. Add the `psql` program to the system path, if needed

   - On Windows:

     - First, find and copy your PostgreSQL bin file-path. The default path is `C:\Program Files\PostgreSQL\version_number\bin`. For example, for version 16, it would be `C:\Program Files\PostgreSQL\16\bin`.
     - Search for and select `"edit the system environment variables"` in the Windows start menu.
     - Towards the bottom of the resulting `"System Properties"` screen, click on `"Environment Variables"`.
     - In the `"System variables"` section on the resulting screen, find the PATH variable and double click or click `"Edit..."`.
     - Click the `"New"` button, and paste your PostgreSQL bin filepath. Click OK. ![Adding psql to PATH on Windows](<../Auxiliary Files/Images/Development_Images/environmentVariablesFull.jpg>)

   - On Linux:
     - Almost all package installs will leave `psql` somewhere in the path. If 
not, consult your shell documentation, as a variety of solutions exist. 
Creating a symlink to `psql` that lives in a path directory should work
 universally, but creating an entry in `.bashrc` also works on bash.

     ***

   - Verify the path is correct by running `psql` from the command line
     - On Linux, you will need to do this as the `postgres` system user,
       much like in Step 2.
     - On Windows, the default system user is `postgres`, so you will need to type `psql -U postgres` to login as user: postgres. Once prompted, enter the superUser password you created during installation. You should now see `postgres=#` in the command line.

5. Once in `psql`, create a user by 
`CREATE USER username WITH PASSWORD 'password';`

   - The exact user and password are at your discretion, but consider creating a
     user specifically for the project to limit access to any other databases 
     you may have on your machine.

6. Create the database for the project by 
`CREATE DATABASE commitment_to_change_app WITH OWNER username;`

   - The name of this database is technically also at your discretion as you will be able to change it in configuration later.

   ![PostgreSQL creation](<../Auxiliary Files/Images/Development_Images/postGres1stlogin.png>)

7. Give your user database creation permissions by 
`ALTER USER username CREATEDB;` so Django can run databse tests.

8. Exit `psql` with `\q` or `CTRL + C`. `\q` is preferred as a soft quit.

---

### Create `custom_settings.py`

1. Create a file called `custom_settings.py` in 
`Commitment_to_Change_App/Commitment_to_Change_App/`, next to `settings.py`.
  - **Do _NOT_ commit this file under any circumstances!** We do not want to 
  know your database or secret key details, which is why it has been separated 
  from `settings.py`!


2. Paste the following into `custom_settings.py`:
```
# Database
# https://docs.djangoproject.com/en/4.2/ref/settings/#databases
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'commitment_to_change_app',
        'USER': 'username',
        'PASSWORD': 'password',
        'HOST': 'localhost',
        'PORT': '',
    }
}

# SECURITY WARNING: keep the secret key used in production secret!
SECRET_KEY = ''
```

3. Run the following code in your terminal to generate a secret key:
```
python -c "import secrets; print(secrets.token_urlsafe())"
```

4. Paste the secret key in Step 3 into the single quotes after `SECRET_KEY` in `custom_settings.py`.

5. Modify the `NAME`, `USERNAME`, and `PASSWORD` keys under `DATABASES` in `custom_settings.py` to match whatever you set them to in [Install and Configure PostgreSQL](#install-and-configure-postgresql).

### Get Django to work with PostgreSQL

1. Install the `psycopg2` Python package by running `pip install psycopg2`.
  - If you opted to install Django system-wide with a package on Linux, consider
  installing `psycopg2` as a package if it is available for consistency. Then
  skip to Step 2.

- ### psycopg2 NOTE:
  - psycopg2 must be installed while your virtual environment is active [as explained here](#important) If it is not, psycopg2 will install in your system site-packages and not in your virtual environment, causing it to be unreachable in your venv.

2. Change to the `Commitment_to_Change_App` directory with `manage.py` in it.
3. Run `python manage.py makemigrations` to create the migrations to be performed.
4. Run `python manage.py migrate` to perform the migrations.

   - Migrate troubleshooting:
     - `ImportError: Couldn't import Django`: This may mean your virtual environment is not currently active. Please activate your environment [as explained here](#important) and try again.
     - `Error loading psycopg2 or psycopg module`: pyscopg2 was probably not installed in your virtual environment. Make sure to install it while your environment is activated, [as explained above](#psycopg2-note).

---

# Configuring your IDE

## PyCharm

### Opening the project in PyCharm

1. Open PyCharm and close any already-open projects.
2. In the Projects tab, select "Open"
3. Navigate to the root directory you cloned the project into.

   - When listing files and dirs in this directory, you should see a directory "Commitment_to_Change_App" but not a directory "commitments".

4. Click OK.

### PyCharm troubleshooting
- Linting errors for Django stuff (for example, `Course.objects` is highlighted
saying that Course has no such field) in Community Edition:
  - This problem is due to Community Edition not supporting the Django framework.
  There are three solutions to this problem:
    1. Get the Professional Edition
    2. Use VSCode instead 
    3. Manually suppress these problems and trust that the if the code runs 
    without crashing or bugs, the errors are not so important after all.

---

## VSCode

### Opening the project in VSCode

1. Open VSCode and close any already-open projects.
2. Click "File" -> "Open File" from the context menu.
3. Navigate to the root directory you cloned the project into. Select "Commitment-to-Change-App"

   - You'll know you're in the correct directory if inside you see a directory named "Commitment_to_Change_App" but not a directory named "commitments".

4. Click OK.
#### Alternative launching to use venv
This has been tested on Linux only.
1. While your virtual environment is active in the shell, navigate to the root
directory of the project containing `.gitignore`
2. Execute `code .`
3. Alternative, navigate to the directory with `manage.py` and execute `code ..`

### VSCode troubleshooting

- Yellow error squiggles underlining imports or other code:![Alt text](<../Auxiliary Files/Images/Development_Images/vscode_enterInterpreterPath.png>)

  - To fix this, you'll need to switch from using the globally installed Python.exe as your interpreter, to your local venv Python install.
  - Click the Python version number in the bottom right of the page, or mouse over a line with error squiggles, select "Quick Fix...", then "select a different interpreter". Click "+ Enter interpreter path" in the top bar, then "Find...", and navigate to your venv's Scripts folder, and click on Python.

- Problems with linting around Django stuff:![Alt text](<../Auxiliary Files/Images/Development_Images/vscode_pylint_django_linting_problem.png>)
  - These errors occur because by default, pylint does not understand some 
Django functionality, particularly Django models.
  - Install `pylint` and `pylint-django` to your project venv with pip.
  - The following should be added to your `settings.json`:
```
    "pylint.args": [
        "--loadplugins=pylint_django",
        "--django-settings-module=Commitment_to_Change_App.settings",
    ]
```

---

# Testing the environment and app (Manual replication)

If you're using Windows, use the specific steps for Windows.

Otherwise, use the general steps and consult your specific OS's documentation for specific terminal commands.

## Unit & Integration Testing

1. Activate the environment using the instructions in [Full Stack Testing](#full-stack-testing)

2. Instead of starting the server with `python manage.py runserver`, run 
`python manage.py test`

### Location of Unit and Integration tests

In each app there is a `test.py` files where all automated tests are located.

## Full Stack Testing

1. Activate the environment and run the Django server.

   - ### General steps

    - Activate

     - Open a terminal window in your IDE or elsewhere, navigate to your project's virtual environment root folder, and run activate.bat in the Scripts directory.
     - Navigate down to `Commitment-to-Change-App` then to `Commitment_to_Change_App`. You'll know you're in the correct directory if there is a `manage.py` file.
     - Start up the django server by running `py manage.py runserver`.

     ***

   - ### Specific steps for Windows Command Prompt (CMD)

     - While in your route directory, type `Scripts\activate.bat`
     - Then navigate down the directory with `cd Commitment-to-Change-App\Commitment_to_Change_App`. You can then type `dir` to check for the `manage.py` file.
     - Now type `py manage.py runserver`
       ![Alt text](<../Auxiliary Files/Images/Development_Images/WindowsCMDSteps.png>)

---

2. Open a web browser and navigate to `localhost:8000/app/register/clinician/`
    - Fill out the form to register a user

---

3. Navigate to `/localhost:8000/accounts/login/`
    - Login with the user you just registered

---

4. Navigate to `localhost:8000/app/commitment/make/`


- Fill out the commitment and hit "Submit" to view the commitment.

---

5. If all of these steps proceed without issue, you can generally consider your environment functional.



# Troubleshooting

## SSL Errors When Using Join Links

These come from Django not running SSL. Just make it `http` instead of `https`. We are leaving it as `https` to avoid 
the possibility of leaving it `http` for deployment and potentially causing security issues. A production environment 
would use `https` only.

## Migrating When Updating from Git

Whenever you update the project and notice changes, it is advisable to run migrations with
```
python manage.py makemigrations
python manage.py migrate
```
as any changes to the models require this. If you are worried about your database, consider creating a new one to test the new code on. Follow the database wipeout procedure below, but with the following exceptions:
- Backup every numbered file in the `migrations` folders before deleting them
- Do not run the `DROP DATABASE commitment_to_change_app;` command
- Run `CREATE DATABASE commitment_to_change_app2 WITH OWNER username;` to create
a new database with a different name but same owner
- Update the database name in `database_authentication.py` to use your new database

In this way, you always have your old database and migrations and can restore them to manually migrate if need be.

## Database Wipeout Procedure

In some cases, figuring out migrations for existing objects can be more effort than simply recreating a fresh database. The following steps need to be performed to do this:

1. Remove every numbered file in the `migrations` folders - for example, `0001_*py`
    - Do NOT remove `__init__.py` from these folders.
2. Open `psql`
3. Run `DROP DATABASE commitment_to_change_app;`
4. Run `CREATE DATABASE commitment_to_change_app WITH OWNER username;`
    - Replace `username` with the username you used in original creation
5. Exit `psql` with `\q`
6. Run `python manage.py makemigrations`
7. Run `python manage.py migrate`
8. Test the server with `python manage.py runserver`
