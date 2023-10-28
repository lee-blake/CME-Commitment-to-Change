# Replicating the Environment

## Environment Overview

## Replication Instructions

If you are using Linux and already have Python installed, [click here to skip ahead](#install-and-setup-virtual-environment)

---

### Install Python

1. Download Python

   - Python is not included by default in Windows or Mac, so it must be downloaded and installed from: https://www.python.org/downloads/
   - To check if you have Python installed, type `python --version` into a Command Prompt. If Python is installed correctly, this command should return the currently installed Python version.
   - Download the latest Python version that is supported by Django. We are currently using Django version 4.2, so Python version 3.11.6 is the latest supported version.
     - You can check Python/Django version compattibility here: https://www.python.org/downloads/

2. Install Python

   - In the installation dialogue, make sure to check "Add python.exe to PATH". This allows us to execute Python in the command line by simply typing "python" or "py" instead of navigating to it's install location.![python install](<../Auxiliary Files/Images/Python_addToPath.png>)
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
   - You should see 3 folders, `Include`, `Lib`, and `Scripts`, as well as a `pyvenv.py` file. ![venv folder](<../Auxiliary Files/Images/checkvenvCreatedSucceessfully.png>)

3. Activate your virtual environment.

- #### IMPORTANT:

  - You will need to activate your virtual environment BEFORE you run the project, EVERY TIME you run the project.
  - While in your new project root directory, type `Scripts\activate.bat`
  - You should now see something like `(Project_name)` before your project path in the command line. This means you are now in your active virtual environment.

    ![venv activated](<../Auxiliary Files/Images/ActivateBat.png>)

---

### Install Django

1. Install the latest version of Django

   - This may be done via Pip or (on some Linux distributions) a package installation. Pip is generally preferred due to venv.
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

   - Your root folder/venv folder structure should now look similar to this:![Root directory](<../Auxiliary Files/Images/FinalRootFolderStructure.png>)

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
     - Click the `"New"` button, and paste your PostgreSQL bin filepath. Click OK. ![Adding psql to PATH on Windows](<../Auxiliary Files/Images/environmentVariablesFull.jpg>)

     ***

   - Verify the path is correct by running `psql` from the command line
     - On Linux, you will need to do this as the `postgresql` system user,
       much like in Step 2.
     - On Windows, the defualt system user is `postgres`, so you will need to type `psql -U postgres` to login as user: postgres. Once prompted, enter the superUser password you created during installation. You should now see `postgres=#` in the command line.

5. Once in `psql`, create a user by `CREATE USER username WITH PASSWORD 'password';`

   - The exact user and password are at your discretion, but consider creating a
     user specifically for the project to limit access to any other databases you
     may have on your machine.

6. Create the database for the project by `CREATE DATABASE commitment_to_change_app WITH OWNER username;`

   - The name of this database is technically also at your discretion as you will be able to change it in configuration later.

   ![PostgreSQL creation](<../Auxiliary Files/Images/postGres1stlogin.png>)

7. Exit `psql` with `CTRL + C`

---

### Get Django to work with PostgreSQL

1. Install the `psycopg2` Python package by running `pip install psycopg2`.

- ### psycopg2 NOTE:
  - psycopg2 must be installed while your virtual environment is active [as explained here](#important) If it is not, psycopg2 will install in your system site-packages and not in your virtual environment, causing it to be unreachable in your venv.

2. In `Commitment-to-Change-App/Commitment_to_Change_App/Commitment_to_Change_App`, create a file called `database_authentication.py`. You will know it is in the right place if it lives in the same directory as `settings.py`, `asgi.py`, and `wsgi.py`
   ![Database_Authentication file location](<../Auxiliary Files/Images/database_authenticationLocation.png>)
3. Put the following in `database_authentication.py`, subject to whatever you did when installing and configuring PostgreSQL:

```
POSTGRESQL_DATABASE_NAME = 'commitment_to_change_app'
POSTGRESQL_DATABASE_USERNAME = 'username'
POSTGRESQL_DATABASE_PASSWORD = 'password'
```

- **Do _NOT_ commit this file under any circumstances!** We do not want to know your database authentication details, which is why it has been separated from `settings.py`!

4. Change to the `Commitment_to_Change_App` directory with `manage.py` in it.
5. Run `python manage.py makemigrations` to create the migrations to be performed.
6. Run `python manage.py migrate` to perform the migrations.

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

   - When listing files and dirs in this directory, you should see a directory "Comittment_to_Change_App" but not a directory "commitments".

4. Click OK.

---

## VSCode

### Opening the project in VSCode

1. Open VSCode and close any already-open projects.
2. Click "File" -> "Open File" from the context menu.
3. Navigate to the root directory you cloned the project into. Select "Commitment-to-Change-App"

   - You'll know you're in the correct directory if inside you see a directory named "Comittment_to_Change_App" but not a directory named "commitments".

4. Click OK.

### VSCode troubleshooting

- Yellow error squiggles underlining imports or other code:![Alt text](<../Auxiliary Files/Images/vscode_enterInterpreterPath.png>)

  - To fix this, you'll need to switch from using the globally installed Python.exe as your interpreter, to your local venv Python install.
  - Click the Python version number in the bottom right of the page, or mouse over a line with error squiggles, select "Quick Fix...", then "select a different interpreter". Click "+ Enter interpreter path" in the top bar, then "Find...", and navigate to your venv's Scripts folder, and click on Python.

---

# Testing the environment and app

If you're using Windows, use the specific steps for Windows.

Otherwise, use the general steps and consult your specific OS's documentation for specific terminal commands.

---

1. Activate the environment and run the Django server.

   - ### General steps

     - Open a terminal window in your IDE or elsewhere, navigate to your project's virtual environment root folder, and run activate.bat in the Scripts directory.
     - Navigate down to `Commitment-to-Change-App` then to `Commitment_to_Change_App`. You'll know you're in the correct directory if there is a `manage.py` file.
     - Start up the django server by running `py manage.py runserver`.

     ***

   - ### Specific steps for Windows Command Prompt (CMD)

     - While in your route directory, type `Scripts\activate.bat`
     - Then navigate down the directory with `cd Commitment-to-Change-App\Commitment_to_Change_App`. You can then type `dir` to check for the `manage.py` file.
     - Now type `py manage.py runserver`
       ![Alt text](<../Auxiliary Files/Images/WindowsCMDSteps.png>)

---

2. Open a web browser and navigate to `LocalHost:8000/app/commitment/new`

   ![Commitment Creation Form](<../Auxiliary Files/Images/CommitmentCreationForm.png>)

- Fill out the commitment and hit "Submit".

  ![Commitment Redirect](<../Auxiliary Files/Images/CommitmentCreatedConfirmationScreen.png>)

- Click the link to view the commitment.

  ![Commitment View](<../Auxiliary Files/Images/CommitmentView.png>)
