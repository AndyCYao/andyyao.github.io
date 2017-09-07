---
layout: default
title: "Deploying a Flask App in an Apache server"
date: 2017-09-07
categories: Deploy
---

I want to have a place on my website to host the recommender app. The app is written in Python and Jquery. Below are the necessary steps so far to get it up and running. 

1. SSH into the ubuntu box
2. go to /var/www
3. mkdir FlaskApps/Recommender
4. Git Clone the app into here. 
5. in /var/www/FlaskApps create a .wsgi file with below 

~~~python
#! /usr/bin/python
import sys
import logging
logging.basicConfig(stream=sys.stderr)
sys.path.insert(0,"/var/www/FlaskApps/Recommender/") # working one
# sys.path.insert(0, "/var/www/FlaskApps/")

# home points to the home.py file
from app import app as application
application.secret_key = "secretKey"
~~~

6. go to /etc/apache2 create a Recommender.conf file with the below 

~~~
<VirtualHost *:80>
    ServerName www.andy-yao.com
    ServerAdmin admin@mywebsite.com
    WSGIScriptAlias /recommender /var/www/FlaskApps/FlaskApps.wsgi
    <Directory /var/www/FlaskApps/Recommender/>
        Order allow,deny
        Allow from all
    </Directory>
    <Directory /var/www/FlaskApps/Recommender/static/>
        Order allow,deny
        Allow from all
    </Directory>
    ErrorLog ${APACHE_LOG_DIR}/error.log
    LogLevel warn
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
~~~

7. Enable the site by running

~~~
sudo a2ensite Recommender
~~~

7. restart apache and reload to see the changes with the below line 

~~~
sudo service apache2 reload
sudo /etc/init.d/apache2 reload
~~~