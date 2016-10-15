---
layout: post
title: Deploy Flask App on docker
category: python
permalink: python/flask_set_up
---

## Install Apache on docker

If you want to develope a web application, it's necessary to build a dev enviroment. In this tutorial, I'll introduce you how to build a dev enviroment via docker.

This tutorial mostly follows [sentdex's](https://pythonprogramming.net/creating-first-flask-web-app/) tutorial. But I fix some bugs in my enviroment.

**Acutally, you can use DockerFile to do the following work automatically. I'll introduce it in the end.**

### Step 0:Build a container

{% highlight bash %}
sudo docker run -i -t -p 80:5000 --name flask ubuntu:16.04 /bin/bash
{% endhighlight %}

### Step 1: Install a editor

As docker doesn't have default editor, you need to install by yourself.
{% highlight bash %}
apt-get update
apt-get upgrade
apt-get install nano
{% endhighlight %}

### Step 2: Install apache2

You need to install apache.
{% highlight bash %}
apt-get install apache2 
{% endhighlight %}

### Step 3: Install and Enable mod_wsgi
{% highlight bash %}
apt-get install libapache2-mod-wsgi python-dev
a2enmod wsgi
{% endhighlight %}

### Step 4: Creating a Flask Enviroment
{% highlight bash %}
cd /var/www
mkdir FlaskApp
cd FlaskApp
{% endhighlight %}

### Step 5: Creating a Flask Application directory
{% highlight bash %}
mkdir FlaskApp
cd FlaskApp
mkdir static
mkdir templates
{% endhighlight %}

### Step 6: Creating a Flask App
{% highlight bash %}
nano __init__.py
{% endhighlight %}
{% highlight python %}
from flask import Flask

app = Flask(__name__)

@app.route('/')
def homepage():
    return "Hi there, how ya doin?"


if __name__ == "__main__":
    app.run()
{% endhighlight %}

### Step 7: Install Flask

Actually, you dont' need to install flask via virtualenv.

But I suggest you use virtualenv.

Make sure that you'r directory is /var/www/FlaskApp/FlaskApp
{% highlight bash %}
apt-get install python-pip
pip install virtualenv
virtualenv venv
source venv/bin/activate
pip install Flask
python __init__.py
{% endhighlight %}

If it works correctly, congratulation.

### Step 8: Set up Flask configuration file
{% highlight bash %}
nano /etc/apache2/sites-available/FlaskApp.conf
{% endhighlight %}
{% highlight bash %}
<VirtualHost *:80>
                ServerName yourdomain.com, every container will be assigned a ip, get it by docker inspect
                ServerAdmin youemail@email.com
                WSGIScriptAlias / /var/www/FlaskApp/flaskapp.wsgi
                <Directory /var/www/FlaskApp/FlaskApp/>
                        Order allow,deny
                        Allow from all
                </Directory>
                Alias /static /var/www/FlaskApp/FlaskApp/static
                <Directory /var/www/FlaskApp/FlaskApp/static/>
                        Order allow,deny
                        Allow from all
                </Directory>
                ErrorLog ${APACHE_LOG_DIR}/error.log
                LogLevel warn
                CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
{% endhighlight %}
{% highlight bash %}
a2ensite FlaskApp
a2dissite 000-default
service apache2 reload
{% endhighlight %}

### Step 9: Configure WSGI file
{% highlight bash %}
cd /var/www/FlaskApp
nano flaskapp.wsgi
{% endhighlight %}
{% highlight python %}
activate_this = '/path/to/virtualenv/bin/activate_this.py'
execfile(activate_this, dict(__file__=activate_this))

import sys
import logging
logging.basicConfig(stream=sys.stderr)
sys.path.insert(0,"/var/www/FlaskApp/")

from FlaskApp import app as application
application.secret_key = 'your secret key'
{% endhighlight %}

Finally, you need to restart appache.
{% highlight bash %}
service apache2 restart
{% endhighlight %}