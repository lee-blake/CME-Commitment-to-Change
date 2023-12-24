# Replicating the Environment (Docker)

This is the recommended replication method; however, if you really hate Docker, 
consult the instructions for [replicating manually](#replicating-the-environment-manual).

## Replication Instructions

### Install Docker Compose

#### Linux Install

- Most Linux distributions have a package for Docker Compose and you should consult
your distributions documentation for installing it.
  - On Arch, install `docker-compose` with pacman.
    - You will need to run `docker-compose` instead of `docker compose`
- You should ensure your user is added to the `docker` group if you want to run without sudo.
  - If you do not want to log out, run `su <your username>` before executing
  Docker commands
  - Note that this will mean that you are root for all intents and purposes.
- On systemd machines, you should ensure the Docker daemon is started before
executing commands.
  - Start it manually or implement one of the two options given 
  [here](https://wiki.archlinux.org/title/Docker#Installation).

#### Windows install
- Docker-compose is included with Docker by default in the installer.
- Download the Docker installer [from Docker.com](https://www.docker.com/products/docker-desktop/) and follow the prompts. A restart will be required to finish installation.
- All default settings during installation and setup are fine.


### Clone the Main Code Repo

1. Navigate to the directory you want the root of the project to live in. All
   future paths will be relative to this directory.
2. Run
   `git clone https://github.com/lee-blake/Commitment-to-Change-App.git`
   in the desired directory to clone to.
3. Change into the root of the the project (via `cd Commitment-to-Change-App`). All future
paths will be relative to this directory unless otherwise specified.

### Create `custom_settings.py` (Docker)

1. Copy `Commitment_to_Change_App/Commitment_to_Change_App/custom_settings_sources/custom_settings_docker.py`
  to `custom_settings.py` in `Commitment_to_Change_App/Commitment_to_Change_App/`,
  next to `settings.py`. This should give you reasonable defaults for your Docker setup.
- **Do _NOT_ commit this file under any circumstances!** We do not want to 
  know your secret key details, which is why it has been separated 
  from `settings.py`!
2. Run the following code in your terminal to generate a secret key:
  `python -c "import secrets; print(secrets.token_urlsafe())"`

3. Paste the secret key in Step 2 in between single quotes after `SECRET_KEY` 
in `custom_settings.py`.

### Build the Docker Containers

1. Run `docker compose build`.
2. Initialize the containers with `docker compose up`. Terminate the process with `CTRL - C`
a few seconds after it stops printing to the console.

### Perform Migrations (Docker)

1. Run the following commands:
```
docker compose start
docker compose exec -it cme-ctc-web python manage.py makemigrations
docker compose exec -it cme-ctc-web python manage.py migrate
docker compose stop
```


### Verify the App

1. Verify the app runs with `docker compose up`.
  - On your host machine, navigate to `127.0.0.1:8000` and check that the welcome/login page shows.
  - You may need to run this twice because the database can be slow to 
  initialize the first time.

2. You should perform all of the tests specified 
[here](#testing-the-environment-and-app-with-docker).

3. Once this is done, you can consider the replication step complete.
Proceed to [configure your IDE](#configuring-your-ide).

## Docker-Specific Considerations

Since under Docker replication the database is in a container, all operations
involving it should generally be done in the Docker containers unless there
is an extremely compelling reason not to. This means that migrations and 
test runs should be done in the container. It can be particularly annoying
to frequently type things like 
```
docker compose start
docker compose exec cme-ctc-web pytest
docker compose stop
```
so automation via scripts is strongly recommended. See the section below for how
to do so is strongly recommended.


### Migrating in Docker

You will need to start the containers to conduct migrations, like was done [above](#perform-migrations-docker). 
This is because both the Python execution environment and PostgreSQL live in containers.

As this process requires multiple longer commands, it is recommended that you write some scripts 
to help condense it for you. 

### General Script Tips

**Convenience scripts should generally be put in `dev_scripts` so they are 
not tracked.**

- ***WARNING: You should not use `docker compose run` because that makes a new container every time.***
- If you want an interative terminal (for example, with `psql`) you must use
`docker compose exec -it <container> <command>` or else the script will just 
execute without any further input from you.

### Scripts (Linux)

Here are some possible scripts you can make to avoid lots of typing. Testing & coverage 
scripts are including in [Testing the environment and app](#testing-the-environment-and-app-with-docker)

#### Make migrations & migrate
```
docker compose start
docker compose exec -it cme-ctc-web python manage.py makemigrations
docker compose exec -it cme-ctc-web python manage.py migrate
docker compose stop
```
  - **Make sure to not forget the `-it` option for `makemigrations` because you may need to input values!**

#### Run general commands from `manage.py` in the container
```
docker compose start
docker compose exec -it cme-ctc-web python manage.py "$@"
docker compose stop
```
  - *NEVER* use this to run the server, `docker compose up` already does that for you.
  - If this script had relative path `developer_scripts/manage`, you would call 
  it like `developer_scripts/manage test` to run tests, or `developer_scripts/manage makemigrations cme_accounts`
  - **Make sure to not forget the `-it` option for `makemigrations` because you may need to input values!**

#### Get a `psql` terminal to run commands in for the main database
```
docker compose start
docker compose exec -it cme-ctc-db psql -U postgres postgres
docker compose stop
```

### Scripts (Windows)

In theory, any script that [works on Linux](#scripts-linux) should also work on Windows if it consists solely of
commands that start with `docker compose`, as long as it is in a `.bat` file. Repeats of these scripts are thus 
omitted here for brevity.

# Testing the environment and app (with Docker)

Currently, our unit and integration testing is quite poor. You should both run
the automated tests and perform a manual full-stack test of all features.

## Run the Automated Tests (Docker)

- If the containers are not up, run 
```
docker compose start
docker compose exec cme-ctc-web pytest
docker compose stop
```
- Otherwise you could instead run
`docker compose exec cme-ctc-web pytest`
in another terminal.

### Running with Coverage (Docker)
Run
```
docker compose start
docker compose exec cme-ctc-web coverage -m pytest
docker compose exec cme-ctc-web coverage report
docker compose stop
```
## Full-stack Testing (Docker)

Run `docker compose up` if your containers are not up and perform the feature 
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
14. Using `docker compose exec -it cme-ctc-db psql -U postgres postgres` in 
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

## Linting (Docker)
You should lint your code prior to opening a pull request using the same settings that the CI does. The config files are included
with the code. If you are running on Docker, you can easily bundle the various linting commands into a single script as below, but splitting them can work too (just remember to start and stop the containers). Alternatively, you can run the commands on your local machine using the instructions [here](#linting-manual) (requires installing the `requirements.txt` modules globally or in a venv).

### Run all linting commands in one go
```
docker compose start
docker compose exec cme-ctc-web djlint .
docker compose exec cme-ctc-web pylint .
docker compose stop
```

---

# Replicating the Environment (Manual)

This method is trickier than [Replicating with Docker](#replicating-the-environment-docker) and is not recommended outside
of deployment.

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
   - Download the latest Python version that is supported by Django. *We are currently using Django version 4.2, so Python version 3.11.6 is the latest supported version*.
     - You can check Python/Django version compatibility here: https://www.python.org/downloads/

2. Install Python

   - In the installation dialogue, make sure to check "Add python.exe to PATH". This allows us to execute Python in the command line by simply typing "python" or "py" instead of navigating to it's install location.
   ![python install](<../Auxiliary Files/Images/Development_Images/Python_addToPath.png>)
     If you forget to check this, you can manually add to PATH later,
     [similarly to how we will do it with PSQL](#install-and-configure-postgresql)
   - Click "install now"
   - Ignore the "Disable path length limit" option shown at the end of installation.

3. Verify Python installation

   - Use `python --version` to verify installation.
   - The Python installer includes the Python package manager, known as pip. You can check if pip is installed and list installed packages by using the following command: `pip list`
   - If pip is not installed, use the command `py get-pip.py` or reinstall python and ensure your PATH is correctly updated. 

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

### Install and Configure PostgreSQL

If you would prefer not to install a database **(not recommended)** you may skip this step. See [this section](#consider-a-memory-only-database) for some drawbacks to this choice.

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

3. Start the PostgreSQL service if needed (some Linux only)

   - On `systemd` Linux systems, use `sudo systemctl start postgresql`. You may also want to run `sudo systemctl enable postgresql` if you do not want to run the start command every time.
   - This isn't needed on Ubuntu 22.04.

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
`ALTER USER username CREATEDB;` so Django can run database tests.

8. Exit `psql` with `\q` or `CTRL + C`. `\q` is preferred as a soft quit.

9. Note that you may need to start the service again if you reboot. This will depend on your system and if it is needed,
you should use the strategy you used above to start it the first time.

---

### Clone the Main Code Repo

1. Navigate to the directory you want the root of the project to live in. All
   future paths will be relative to a child of this directory.
   - NOTE: This must be inside the virtual environment directory [you created earlier](#install-and-setup-virtual-environment).
2. Run
   `git clone https://github.com/lee-blake/Commitment-to-Change-App.git`
   in the desired directory to clone to.

   - Your root folder/venv folder structure should now look similar to this:![Root directory](<../Auxiliary Files/Images/Development_Images/FinalRootFolderStructure.png>)
3. Change into the root of the the project (via `cd Commitment-to-Change-App`). All future
paths will be relative to this directory unless otherwise specified.

---

### Install requirements with pip

1. Navigate to the directory `Commitment_to_Change_App`. You will know when you are in the right directory when you can
see `manage.py`.
2. Run `pip install -r requirements.txt`.
   - **Make sure your virtual environment is active for this step!**
     
#### Test Django installation (Optional)
You can verify that Django installed correctly with the following steps
1. While your virtual environment is active, navigate outside of the project files somewhere where you
don't mind writing some files temporarily.
3. Create a test project using `django-admin startproject testproject`

   - This MUST be done in the directory you intend to clone the project into.

4. Change into the `testproject` directory
5. Run the Django server with `python manage.py runserver`
6. Connect to `localhost:8000` to verify that Django is running
7. Shut down the server by typing `CTRL + C`
8. Recursively remove the `testproject` directory

---

### Create `custom_settings.py` (Manual)

1. Copy `Commitment_to_Change_App/Commitment_to_Change_App/custom_settings_sources/custom_settings_manual.py`
  to `custom_settings.py` in `Commitment_to_Change_App/Commitment_to_Change_App/`,
  next to `settings.py`. This should give you reasonable defaults for your Docker setup.
  - **Do _NOT_ commit this file under any circumstances!** We do not want to 
  know your secret key details, which is why it has been separated 
  from `settings.py`!

2. Run the following code in your terminal to generate a secret key:
```
python -c "import secrets; print(secrets.token_urlsafe())"
```

3. Paste the secret key in Step 2 into the single quotes after `SECRET_KEY` in `custom_settings.py`.

4. Modify the `NAME`, `USERNAME`, and `PASSWORD` keys under `DATABASES` in `custom_settings.py` to match whatever you set them to in [Install and Configure PostgreSQL](#install-and-configure-postgresql).

#### Consider a memory-only database

If you would not like to use a database that writes to disk, you can add the following line to `custom_settings.py` and ignore the other instructions relating to databases:
```
DATABASES = {
    "default": {
        "ENGINE": "django.db.backends.sqlite3",
        "NAME": ":memory:",
    }
}
```
**This is generally not recommended.** The reason is that you will lose all data by shutting down the server. You may even trigger this if Django automatically reloads the server due to code changes (untested, but a possible risk). Since virtually all functions require logging in, which requires an account, which requires email verification, this will make development very annoying very quickly. It is also not suitable for production for obvious reasons. However, this option does exist.

#### Consider your email backend

By default, the manual settings give you Django's console backend, which prints all emails to the console. This is an 
adequate solution for development that does not degrade the production site's email reputation . If you would prefer to 
test that Django actually sends the email out somewhere, the simplest option is probably `aiosmtpd`.
1. Open another console because you will need to run `aiosmtpd` alongside your server
2. Decide whether you want to create a new venv or recycle your existing one. Either way, activate the desired venv.
3. `pip install aiosmtpd`
4. You should be able to run `aiosmtpd -l 127.0.0.1:25 -c aiosmtpd.handlers.Debugging`, but may need to run
`python -m aiosmtpd -l 127.0.0.1:25 -c aiosmtpd.handlers.Debugging` instead.
  - This setup uses port 25. You can change that if desired but it should match the config in Django.
  - This setup rejects anything non-localhost. If you are running Django and `aiosmptd` on different machines
  (for example, VMs) you can change `127.0.0.1` to `0.0.0.0` to accept all hosts.
6. Modify your Django `custom_settings.py` configuration to match with `aiosmtpd`
  - Comment out, delete, or replace the `EMAIL_BACKEND` value with
  `EMAIL_BACKEND = "django.core.mail.backends.smtp.EmailBackend"`
  - Set `EMAIL_HOST = "localhost"` or the address of the other machine
  - Set `EMAIL_PORT = 25` or whatever port you set it to
7. Intercepted emails will now be printed by `aiosmtpd` in its console.

The advantage of this is that you can be sure that Django really does send out those emails. The disadvantage is
the extra setup, plus having to start `aiosmtpd` anytime you want to run the server. Our recommendation is that you
use this check only when your Django version itself is updated, and even then you probably do not really need it.

---

### Perform migrations (manual)

1. Change to the `Commitment_to_Change_App` directory with `manage.py` in it.
2. Run `python manage.py makemigrations` to create the migrations to be performed.
3. Run `python manage.py migrate` to perform the migrations.

   - Migrate troubleshooting:
     - `ImportError: Couldn't import Django`: This may mean your virtual environment is not currently active. Please
     activate your environment [as explained here](#important) and try again.
     - `Error loading psycopg2 or psycopg module`: pyscopg2 was probably not installed in your virtual environment. Make
     sure to install it while your environment is activated, [as explained above](#psycopg2-note).
     - `Thrown exceptions`: If migrations have been made after the initial migrations and there are thrown exceptions,
     the migration changes are stored in the `migrations.py` folders in the project files. These files should be deleted
     minus the `__init.py__` and `py manage.py makemigrations` should be run in the command line again. See [Troubleshooting](#migrating-when-updating-from-git)
     for more troubleshooting tips.
    
---

### Verify the App

1. Verify the app runs with `python manage.py runserver` when in the `Commitment_to_Change_App`
directory with `manage.py` in it.
  - On your host machine, navigate to `127.0.0.1:8000` and check that the welcome/login page shows.

2. You should perform all of the tests specified 
[here](#testing-the-environment-and-app-manual-replication).

3. Once this is done, you can consider the replication step complete.
Proceed to [configure your IDE](#configuring-your-ide).

---
# Testing the environment and app (Manual replication)

If you're using Windows, use the specific steps for Windows.

Otherwise, use the general steps and consult your specific OS's documentation for specific terminal commands.

## Unit & Integration Testing

1. Activate the environment using the instructions in [Full Stack Testing](#full-stack-testing)

2. Run `pytest` in the directory where `manage.py` is located. If coverage is desired, run
```
coverage -m pytest
coverage report
```

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

     ***

2. Open a web browser and navigate to `localhost:8000/app/register/clinician/`
    - Fill out the form to register a user

3. Navigate to `/localhost:8000/accounts/login/`
    - Login with the user you just registered

4. Navigate to `localhost:8000/app/commitment/make/`

- Fill out the commitment and hit "Submit" to view the commitment.

5. If all of these steps proceed without issue, you can generally consider your environment functional.

---

## Linting (manual)
You should lint your code prior to opening a pull request using the same settings that the CI does. The config files are included
with the code. However, they are a directory level down, so you will have to either drop into the top `Commitment_to_Change_App` with `manage.py` or else point the linters to the correct place.

### In `Commitment_to_Change_App`
```
djlint .
pylint .
```

### In the project root
Currently we use the default settings for djlint so it does not need to be pointed to a config file. This may change.
```
djlint Commitment_to_Change_App
pylint Commitment_to_Change_App --rcfile=Commitment_to_Change_App/.pylintrc
```

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
    3. Manually suppress these problems and trust that if the code runs 
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
3. Alternatively, navigate to the directory with `manage.py` and execute `code ..`

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
- Problems with linting imports: If you encounter errors when importing from a module that shares a common ancestor with the file being linted, this is an issue with the `pylint` working directory.
  - For example: If in `commitments.tests.test_models.py` the import of `commitments.models`, pylint says it cannot import,
  then that is an issue of this problem because `test_models.py` and `models.py` both have the `commitments` ancestor package.
  - Solution: Make sure the current working directory for `pylint` contains `manage.py` by modifying the settings.
    - If you run from the repo root, the CWD should be `${workspaceFolder}/Commitment_to_Change_App`.

---

# Troubleshooting

## SSL Errors When Using Join Links

These come from Django not running SSL. Just make it `http` instead of `https`. We are leaving it as `https` to avoid 
the possibility of leaving it `http` for deployment and potentially causing security issues. A production environment 
would use `https` only.

## Migrating When Updating from Git

### With Docker 


Whenever you update the project and notice changes, it is advisable to run migrations with
```
docker compose start
docker compose exec -it cme-ctc-web python manage.py makemigrations
docker compose exec -it cme-ctc-web python manage.py migrate
docker compose stop
```
as any changes to the models require this. If you are worried about the database, it is possible to get a fresh
one without losing your old one by running 
```
docker compose --project-name <another project name> build
docker compose --project-name <same name as above> up
```
and then proceeding to [perform migrations](#perform-migrations-docker) with the same `--project-name`. Note that
every compose operation with this new setup must include the `--project-name` parameter before the compose operation.

### With manual replication

Whenever you update the project and notice changes, it is advisable to run migrations with
```
python manage.py makemigrations
python manage.py migrate
```
as any changes to the models require this. If you are worried about your database, consider creating a new one to test the new code on. Follow the database wipe-out procedure below, but with the following exceptions:
- Backup every numbered file in the `migrations` folders before deleting them
- Do not run the `DROP DATABASE commitment_to_change_app;` command
- Run `CREATE DATABASE commitment_to_change_app2 WITH OWNER username;` to create
a new database with a different name but same owner
- Update the database name in `database_authentication.py` to use your new database

In this way, you always have your old database and migrations and can restore them to manually migrate if need be.

## Database Wipe-out Procedure

In some cases, figuring out migrations for existing objects can be more effort than simply recreating a fresh database. The following steps need to be performed to do this:

### Wipeout (Docker replication)

1. Ensure the containers are all stopped with `docker compose stop`.
2. Run `docker compose rm`.
3. Remove every numbered file in the `migrations` folders - for example, `0001_*py`
    - Do NOT remove `__init__.py` from these folders.
4. Recreate the containers with `docker compose build`
5. Follow the instructions to [Perform Migrations](#perform-migrations-docker)
6. You now have a fresh database on Docker.

### Wipeout (Manual replication)

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
