# Deployment

The following deployment instructions involve deployment to an Apache server as an interim measure. We plan to support cloud deployment in a future iteration.

## Obtain an Apache server with `mod_wsgi`

1. Install and configure a server with `mod_wsgi`
    - An example for Ubuntu can be seen 
[here](https://www.howtoforge.com/how-to-run-python-scripts-with-apache-and-mod-wsgi-on-ubuntu-22-04/).
2. Verify that `mod_wsgi` is working via the instructions in the link above or 
some similar test script.

## Setup the project

The instructions here will assume a Linux install but will use venv.

1. Install and initialize PostgreSQL with the instructions [here](Development.md#install-and-configure-postgresql)
    - Installation of the `postgresql` package on Ubuntu 22.04 does not seem to 
require manual initialization of the database cluster.
2. Create a directory to house the root of the project. For these instructions, that directory will be `/srv/project_root`. Change into that directory.
    - Keep in mind that Apache will need permissions for the directory and its subtree.
3. Create a venv in that directory with the instructions [here](Development.md#install-and-setup-virtual-environment). The example here creates a venv name `project_venv`.
    - On Ubuntu 22.04 you will likely need to install the package `python3-venv`
4. Install [Django](Development.md#install-django) in your virtual environment.
In this example, you should be in the dir `/srv/project_root/project_venv`
    - You should follow the testing steps to ensure Django works locally, but
make sure to return to this directory and remove the testproject when you are done.
5. Follow the instructions to [clone the main code repo](Development.md#clone-the-main-code-repo) 
    - You may need to install git, on Ubuntu this is package `git`.
    - The top `Commitment_to_Change_App` folder will live next to `pyvenv.cfg`
6. Follow the instructions to [get Django to work with PostgreSQL](Development.md#get-django-to-work-with-postgresql)
    - Getting `psycopg2` to build on Ubuntu requires the following packages:
        - Install using `apt-get`: `gcc, python3-dev, libpq-dev`
        - Install using `pip` in your virtual environment: `wheel`
7. Test that the project actually works with Django by first running `python manage.py runserver` and then verifying that the root url redirects by one of the following means:
    - Open your web browser and navigate to `127.0.0.1:8000`. This should 
redirect to a login page and it is very obvious whether the server is working or not.
    - Run `curl -v 127.0.0.1:8000`. The reply should contain `302 FOUND` and have 
the location set to `/accounts/login/`.

## Deploy the application

1. Following the instructions [here](https://docs.djangoproject.com/en/4.2/howto/deployment/wsgi/modwsgi/#basic-configuration), point Apache to your project Django server with the following additions to `httpd.conf` (if not following the example, modify the paths accordingly): 
```
Alias /static/ /srv/project_root/project_venv/Commitment-to-Change-App/Commitment_to_Change_App/static/

<Directory /srv/project_root/project_venv/Commitment-to-Change-App/Commitment_to_Change_App/static>
Require all granted
</Directory>

WSGIScriptAlias / /srv/project_root/project_venv/Commitment-to-Change-App/Commitment_to_Change_App/Commitment_to_Change_App/wsgi.py
WSGIPythonHome /srv/project_root/project_venv
WSGIPythonPath /srv/project_root/project_venv/Commitment-to-Change-App/Commitment_to_Change_App

<Directory /srv/project_root/project_venv/Commitment-to-Change-App/Commitment_to_Change_App>
<Files wsgi.py>
Require all granted
</Files>
```
Avoid giving more permissions than are necessary! The above are sufficient.

2. Start/restart Apache and navigate to `127.0.0.1` in `curl` or your web browser. 
The redirect to a login page should occur. If you are using a web browser, styling should be present; otherwise, test that static files are loading by visiting `127.0.0.1/static/styles.css`.

3. Optionally enable daemon mode using the instructions [here](https://docs.djangoproject.com/en/4.2/howto/deployment/wsgi/modwsgi/#using-mod-wsgi-daemon-mode)

## Configuration and Cleanup

1. In `/srv/project_root/project_venv/Commitment-to-Change-App/Commitment_to_Change_App/Commitment_to_Change_App/settings.py`, 
change `Debug = True` to `Debug = False` to disable Django debug messages.

2. Configure Apache to use SSL and certificates. A general guide may be found 
[here](https://httpd.apache.org/docs/2.4/ssl/ssl_howto.html). **The server 
should never be deployed without SSL because it handles passwords.**

3. Remove any `mod_wsgi` and Django test code from earlier steps if you have not already.

4. Verify the server is accessible from other machines.

5. Perform any additional desired configuration.

# Troubleshooting

## Determining the source of problems

If the instructions above are followed in order with proper testing, then it 
should be relatively straightforward to determine which module is at fault. In
particular, one can always diagnose whether Apache is the source by running
the internal Django server while Apache is stopped and seeing if the errors 
can still be replicated. If not, the problem is somewhere in the Apache 
configuration or server. Otherwise, the problem exists somewhere in Django 
and/or PostgreSQL. 

## Django/PostgreSQL Troubleshooting

This is generally covered in the [Development documentation](Development.md#troubleshooting).

## Apache Troubleshooting

### Log location

Consult `/var/log/apache2/error.log` first, but the other logs in that directory
may also be of use.

### Root route doesn't even return anything

Check `error.log` for errors with a message like the following:
```
Permission denied: mod_wsgi (pid=<number>): Unable to stat Python home /srv/project_root/project_venv/. Python interpreter may not be able to be initialized correctly. Verify the supplied path and access permissions for whole of the path.
```
If these are present, then the problem lies in Apache locating your virtual 
environment. First check that the path listed in the log file is correct. If 
so, the verify that whichever user is running the Apache daemon (using 
`ps aux | grep -e apache` may help find this) can access the venv directory by 
using `sudo -u <apacheuser> ls <path/to/venv>`. If not, change the permissions 
until this does work.

### 403 Errors on root route

If the root route returns a 403 response, there are two likely sources:
1. Bad filesystem permissions leave the Apache daemon unable to access all
files required
2. The Apache server configuration targets the wrong directory such that the
wsgi script resides in a directory under the default rule `Require all denied`

For case 1, try
```
ps aux | grep -e apache
sudo -u <apacheuser> cat <path/to/wsgi/file/in/django>
```
If this fails, **change the access mask on the entire project tree in one 
action.** Otherwise, you may struggle to troubleshoot going forward because 
some files will be accessible while others will not.

For case 2, carefully verify that the Directory rule above points to the same 
place as the WSGIScriptAlias rule. If they do not, this will cause an immediate
`Require all denied`

### Lack of styling on pages

If everything else works fine but styling is not present, then Apache is not
correctly mapping to the static files. Use your browser debugger or `curl` to 
determine whether you are getting 404 or 403 responses on requests for static
files. If it is a 403, troubleshoot using the general principles in the 
[previous section](#403-errors-on-root-route). If it is a 404, you have 
pointed Apache to the wrong directory in both the Alias and Directory rules.
