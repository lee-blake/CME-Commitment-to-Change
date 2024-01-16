# Ubuntu Server Deployment

The following deployment instructions involve deployment to an Apache server (assumed to be running on Ubuntu, although most of these instructions will apply to other Linux distributions). 

You will also need some SMTP service to send email from the server.

## Obtain an Apache server with `mod_wsgi`

1. Install and configure a server with `mod_wsgi`
    - An example for Ubuntu can be seen 
[here](https://www.howtoforge.com/how-to-run-python-scripts-with-apache-and-mod-wsgi-on-ubuntu-22-04/).
2. Verify that `mod_wsgi` is working via the instructions in the link above or 
some similar test script.

## Setup the project

The instructions here will assume a Linux install but will use venv. Note that on Ubuntu 22.04 you have have to type 
`python3` instead of `py` or `python` in the instructions. You should be able to skip installing Python due to 
`mod_wsgi`, but if not, then install as per the [instructions](Development.md#install-python)

1. Install and initialize PostgreSQL with the instructions [here](Development.md#install-and-configure-postgresql)
    - Installation of the `postgresql` package on Ubuntu 22.04 does not seem to 
require manual initialization of the database cluster.
2. Create a directory to house the root of the project. For these instructions, that directory will be `/srv/project_root`. Change into that directory.
    - Keep in mind that Apache will need permissions for the directory and its subtree.
3. Create a venv in that directory with the instructions [here](Development.md#install-and-setup-virtual-environment). The example here creates a venv name `project_venv`. Activate the environment.
    - On Ubuntu 22.04 you will likely need to install the package `python3-venv`
4. Follow the instructions to [clone the main code repo](Development.md#clone-the-main-code-repo) 
    - You may need to install git, on Ubuntu this is package `git`.
    - The top `Commitment_to_Change_App` folder will live next to `pyvenv.cfg`
5. Install the [requirements](Development.md#install-requirements-with-pip) in your virtual environment.
6. You should test that Django installed correctly in your virtual environment to save troubleshooting later. Follow
the instructions [here](Development.md#test-django-installation-optional).
    - In this example, you should be in the dir `/srv/project_root/project_venv` when you run `django-admin` as
    per the instructions.
    - You should follow the testing steps to ensure Django works locally, but
    make sure to return to this directory and remove the testproject when you are done.
6. Follow the instructions to create `custom_settings.py` [here](Development.md#create-custom_settingspy-manual).
    - Do not bother changing your email settings just yet, the console backend will do fine for testing and you
    will configure your actual service later.
7. Perform migrations as instructed [here](Development.md#perform-migrations-manual).
8. Test that the project actually works with Django by first running `python manage.py runserver` and then verifying that the root url redirects by one of the following means:
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

<Directory /srv/project_root/project_venv/Commitment-to-Change-App/Commitment_to_Change_App/Commitment_to_Change_App>
<Files wsgi.py>
Require all granted
</Files>
</Directory>
```
Avoid giving more permissions than are necessary! The above are sufficient. Also note that on Ubuntu `httpd.conf` is actually located at `/etc/apache2/apache2.conf`

2. Start/restart Apache and navigate to `127.0.0.1` in `curl` or your web browser. 
The redirect to a login page should occur. If you are using a web browser, styling should be present; otherwise, test that static files are loading by visiting `127.0.0.1/static/styles.css`.

3. Optionally enable daemon mode using the instructions [here](https://docs.djangoproject.com/en/4.2/howto/deployment/wsgi/modwsgi/#using-mod-wsgi-daemon-mode)

## Configure your email backend

This will vary based on which STMP service you use and you should therefore consult the Django documentation 
[here](https://docs.djangoproject.com/en/4.2/topics/email/), particularly on 
[settings](https://docs.djangoproject.com/en/4.2/topics/email/#smtp-backend). However, at a minimum, 
you will probably need to set the following in `custom_settings.py`:
```
# Explicitly instruct Django to use the default SMTP backend
EMAIL_BACKEND = "django.core.mail.backends.smtp.EmailBackend"
# Server info for your email service
EMAIL_HOST = "server-hostname"
EMAIL_PORT = server_port # Integer
# Your credentials for the server
EMAIL_HOST_USER = "your-username"
EMAIL_HOST_PASSWORD "your-password"
# Your server should be using exactly one of these (don't include both) for security reasons
EMAIL_USE_TLS = True
EMAIL_USE_SSL = True
```

## Configuration and Cleanup

1. In `/srv/project_root/project_venv/Commitment-to-Change-App/Commitment_to_Change_App/Commitment_to_Change_App/settings.py`, 
change `Debug = True` to `Debug = False` to disable Django debug messages.

2. Configure Apache to use SSL and certificates. A general guide may be found 
[here](https://httpd.apache.org/docs/2.4/ssl/ssl_howto.html). **The server 
should never be deployed without SSL because it handles passwords.**

3. Remove any `mod_wsgi` and Django test code from earlier steps if you have not already.

4. Verify the server is accessible from other machines.

5. Perform any additional desired configuration.

6. Restart Apache.

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

### Email server difficulties

If you have difficulty with your email server, follow the instructions for `aiosmtpd` 
[here](Development.md#consider-your-email-backend) and use `aiosmptd` to capture the emails while Apache is running. 
You may need to restart Apache if you change the configuration. If you can do that and see them printing in the console, 
any problems with your email server or your configuration to connect to it and not something in the Django-Apache stack.

# AWS Deployment
This section describes deployment to AWS. They are current to January 2024.

## Required Software
You will need OpenSSH to connect and interact with the EC2 instance.

## Obtain an Ubuntu instance on AWS
1. Obtain and log into an AWS account.
2. Go to the EC2 dashboard
3. Select "Launch instance"

### Instance Settings
Unless otherwise specified, use the default settings.

1. From Quick Start, select Ubuntu and 64-bit x86.
2. Create a new key pair for authentication. You should use `.pem` since the instructions will be using OpenSSH. Save it as instructed. Both RSA and ED25519 should be fine, but these instructions were only tested with ED25519.
3. Edit network settings:
    - Make sure a public IP is enabled.
    - For now, create a security group with the following rules:
        - Both inbound and outbound
        - Allow `All traffic`
        - From `Anwhere-IPv4`
4. Launch the instance.

## Connect to the instance
1. If necessary, start the instance.
2. Navigate to EC2 > Instances > *instance id* > Connect 
3. Follow the SSH instructions
    - In general, `ssh -i "your ssh key" ubuntu@whatever.datacenter.compute.amazonaws.com
    - **The `whatever` bit may change each time!** Always verify it from the EC2 console.
4. Trust the fingerprint.

## Prepare Ubuntu
1. Update the software with `sudo apt-get update` and `sudo apt-get upgrade`.
    - If you get a screen asking what daemons should be restarted, just hit tab to go to "OK" and accept the defaults.
2. Install the required software for the Ubuntu deployment: `sudo apt-get install postgresql git python3-venv apache2 apache2-utils ssl-cert libapache2-mod-wsgi-py3`
    - Again, accept the defaults for daemon restart
3. Shutdown the system with `sudo shutdown now`
4. If you have not already, create a personal access token on GitHub with *only* read access to the contents of the *code* repositories.

## Execute the Ubuntu Server Deployment Instructions
Follow the instructions [above](#ubuntu-server-deployment) with the following modifications:

### Testing Django & Apache
You are in an Ubuntu server instance via ssh, which means one shell and no web browser. You probably could install `tmux` and `lynx` to get around this, but you can make due with `curl`:
```
python manage.py runserver
<CTRL-Z>
bg
curl -v 127.0.0.1:8000
<hit enter once you see the green 302>
fg
<CTRL-C>
```

The Apache method should be nicer, it should not need to be running in a blocking manner like Django. Just use `sudo systemctl restart apache2` if you have changed the config and then `curl -v 127.0.0.1:80`

## Test Remote Access
Once you have verified that the full Apache/Django stack works locally, test it from your host machine by visting `<public-ip>:80`. You will need to add the public IP to the Django option `ALLOWED_HOSTS` in either `settings.py` or `custom_settings.py`.

After this, shutdown the system with `sudo shutdown now`
