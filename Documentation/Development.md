# Replicating the Environment

## Environment Overview

## Replication Instructions

### Install Django

1. Install the latest version of Django
  - This may require installing Python 3.x
  - This may be done by Pip or (on some Linux distributions) a package installation. Pip is generally preferred due to venv.
2. Create a test project using ```django-admin startproject testproject```
  - This MUST be done in the directory you intend to clone the project into.
3. Change into the ```testproject``` directory
4. Run the Django server with ```python manage.py runserver```
5. Connect to ```localhost:8000``` to verify that Django is running
6. Shut down the server
7. Recursively remove the ```testproject``` directory

### Install and Configure PostgreSQL

1. Install the latest version of PostgreSQL
  - On many Linux distributions, this may be done via a package. This is the 
preferred method if available because troubleshooting will likely be better 
documented.
2. Initialize the database cluster.
  - It is unclear if this is necessary on all install methods. Consult the 
notes specific to your platform
  - On most Linux installs, a ``postgres`` user is created and this user must 
be the one to execute the initialization using either ```sudo -u postgres initdb --locale en_US.UTF-8 -E UTF8 -D '/var/lib/postgres/data'``` or using ```su``` to switch to ```postgres``` before running ```initdb --locale en_US.UTF-8 -E UTF8 -D '/var/lib/postgres/data'```
3. Start the PostgreSQL service if needed.
  - On ```systemd``` Linux systems, use ```sudo systemctl start postgresql```. You may also want to run ```sudo systemctl enable postgresql``` if you do not want to run the start command every time.
4. Add the ```psql``` program to the system path, if needed
  - Verify the path is correct by running ```psql``` from the command line
    - On Linux, you will need to do this as the ```postgresql``` system user, 
much like in Step 2.
5. Once in ```psql```, create a user by ```CREATE USER username WITH PASSWORD 'password';```
  - The exact user and password are at your discretion, but consider creating a
user specifically for the project to limit access to any other databases you 
may have on your machine.
6. Create the database for the project by ```CREATE DATABASE commitment_to_change_app WITH OWNER username;```
  - The name of this database is technically also at your discretion as you will be able to change it in configuration later.
7. Exit ```psql```


### Get Django to work with PostgreSQL
1. In ```Commitment_to_Change_App/Commitment_to_Change_Site```, create a file called ```database_authentication.py```. You will know it is in the right place if it lives in the same directory as ```settings.py```, ```asgi.py```, and ```wsgi.py```
2. Put the following in ```database_authentication.py```, subject to whatever you did when installing and configuring PostgreSQL:
```
POSTGRESQL_DATABASE_NAME = 'commitment_to_change_app'
POSTGRESQL_DATABASE_USERNAME = 'username'
POSTGRESQL_DATABASE_PASSWORD = 'password'
```
  - **Do *NOT* commit this file under any circumstances!** We do not want to know your database authentication details, which is why it has been separated from ```settings.py```!
3. Change to the ```Commitment_to_Change_App``` directory with ```manage.py``` in it.
4. Run ```python manage.py migrate``` to perform the migrations.


