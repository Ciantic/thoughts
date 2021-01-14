---
title: 'Installation of MySQL server, MySQLdb, Flup, Lighttpd and Django (Debian etch)'
date: 2008-07-15T04:48:00.000-07:00
oldUrl: "http://ciantic.blogspot.com/2008/07/installation-of-mysql-server-mysqldb.html"
tags : [mysql, flup, django, mysqldb, python2.5, fastcgi, debian, lighttpd]
---

Note: I have not tested it as is, I was writing this afterwards from memory, so beware of the errors.

### Setting up debian

  
```bash
# logged in as root:  
apt-get install sudo  
adduser joe  
sudoedit /etc/sudoers  
joe ALL=(ALL) ALL # added this line  
  
# Following is done in my own user (joe):  
sudo apt-get upgrade  
sudo dpkg-reconfigure locales  
sudo tzselect  
sudo apt-get install build-essential  

```  
  

### Now to the installing Django and others...

  
```bash
# Python 2.5  
sudo apt-get install python2.5  
sudo rm /usr/bin/python  
sudo ln -s /usr/bin/python /usr/bin/python2.5  
  
python  
Python 2.5 (release25-maint, Dec  9 2006, 14:35:53)  
[GCC 4.1.2 20061115 (prerelease) (Debian 4.1.1-20)] on linux2  
Type "help", "copyright", "credits" or "license" for more information.  
>>>  
  
# Storing downloaded/compiled python-modules:  
sudo mkdir /usr/src/python-modules   
  
  
# MySQL server:  
sudo apt-get install mysql-server  
  
# MySQLdb:  
# Dependencies:  
sudo apt-get install libmysqlclient15-dev  
sudo apt-get install python2.5-dev  
  
cd /usr/src/python-modules/  
sudo wget http://mesh.dl.sourceforge.net/sourceforge/mysql-python/MySQL-python-1.2.2.tar.gz  
sudo tar -xvzf MySQL-python-1.2.2.tar.gz  
cd MySQL-python-1.2.2  
python setup.py build  
sudo python setup.py install  
cd /usr/src/python-modules/  
  
python  
>>> import MySQLdb  
>>>  
  
  
# Flup (for the fastcgi):  
cd /usr/src/python-modules/  
svn co http://svn.saddi.com/flup/trunk/ flup-svn  
cd flup-svn  
sudo python setup.py install  
cd /usr/src/python-modules/  
  
python  
>>> import flup  
>>>  
  
  
# Lighttpd (1.4.19) installation using Debian unstable repository:  
# TODO: Coming...  
  
# NOTE: My installation method of Django allows to use both, svn and release  
# Django as far as you always run the wanted django using env PYTHONPATH...  
# Django release installation:  
cd /usr/src/python-modules/  
sudo wget http://www.djangoproject.com/download/0.96.2/tarball/ # this one downloads Django-0.96.2.tar.gz  
sudo tar -xvzf Django-0.96.2.tar.gz  
  
env PYTHONPATH=$PYTHONPATH:/usr/src/python-modules/Django-0.96.2 python  
>>> import django  
>>>  
  
# Django svn installation:  
cd /usr/src/python-modules/  
sudo svn co http://code.djangoproject.com/svn/django/trunk/ Django-svn  
  
env PYTHONPATH=$PYTHONPATH:/usr/src/python-modules/Django-svn python  
>>> import django  
>>>  
  
# Django new project and fastcgi server:  
sudo mkdir /var/www-domains/  
  
sudo adduser examplecom  
sudo mkdir /var/www-domains/example.com/  
sudo chown examplecom:examplecom /var/www/example.com  
sudo chmod +s /var/www/example.com  
  
sudo su examplecom  
cd /var/www/example.com/  
mkdir public  
mkdir public_media  
mkdir fastcgi-servers  
mkdir django-projects  
  
# TODO: More to come...  

```