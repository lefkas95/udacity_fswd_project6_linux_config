# Linux Server Configuration

Final project for part 5 of Udacity Fullstack Web Developer Nano Degree.

## Connecting to the server
You can reach the web server under the IP address `http://35.177.235.145`.

To connect to the server itself use SSH with the following command: `ssh grader@35.177.235.145 -p 2200 -i 'path/to/attached/key'`

You can find the necessary SSh key in the repo. Store it somewhere and use the absolute path to it in the above command.

## Installed software
The following stuff was installed using `apt-get` in order to server the web page:

* python
* python pip - to manage python-related packages: flask, requests, psycopg2, oauth2client
* apache2 - To serve the web page
* libapache2-mod-wsgi - To serve a python project
* postgresql - Database

## Configurations
The following configuration was done:

* Create new user 'grader' with root permission
* Configure Amazon Lightsail environment to allow port 2200.
* Add ssh key to the user, password login is disabled in file `/etc/ssh/sshd_config`
* Change SSH port from `22` to `2200` in file `/etc/ssh/sshd_config`
* updated all packages using `sudo apt-get update` and `sudo apt-get upgrade`
* Set up firewall `ufw` to default deny any incoming and allow any outgoing, then opened incoming ports 80 (www), 123 (NTP) and 2200 (before configured port for SSH)
* Write wsgi script to serve the catalog application (include correct path using `sys`)
* Configure postgresql: Create new user 'catalog' to access data, give this user permission to access and edit the table in the database `catalog`
* Configure `wsgi` in file `/etc/apache2/sites-enabled/000-default.conf` by adding `WSGIScriptAlias / /var/www/html/myapp.wsgi` inside the `VirtualHost *:80` tag
* Restart Apache using `sudo apache2ctl restart`

## Used resources
The following resources helped me finish the project:

* Udacity course
* http://flask.pocoo.org/docs/0.12/deploying/mod_wsgi/
* https://httpd.apache.org/docs/
* https://www.postgresql.org/docs/
* http://docs.sqlalchemy.org/en/latest/core/engines.html
* https://packages.ubuntu.com
* https://www.jakowicz.com/flask-apache-wsgi/

Forum posts:

* https://forums.aws.amazon.com/thread.jspa?threadID=160352
* https://stackoverflow.com/questions/15520361/permission-denied-for-relation