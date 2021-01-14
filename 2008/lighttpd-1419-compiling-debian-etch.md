---
title: 'Lighttpd 1.4.19 compiling (Debian etch)'
date: 2008-07-16T02:05:00.000-07:00
oldUrl: "http://ciantic.blogspot.com/2008/07/lighttpd-1419-compiling-debian-etch.html"
---

Following explains briefly how I managed to compile and run Lighttpd.  
  
Remember that this doesn't include init.d scripts and such, and is not great idea for production servers.  
  
Using Debian repository installation of Lighttpd is advised, seek the older article of installing Django, I have exaplained it there.  

```
# Dependencies:  
sudo apt-get install libpcre3  
sudo apt-get install libpcre3-dev  
sudo apt-get install zlib1g  
sudo apt-get install zlib1g-dev  
  
# Compilation:  
cd /usr/src/  
sudo wget http://www.lighttpd.net/download/lighttpd-1.4.19.tar.gz  
sudo tar -xvzf lighttpd-1.4.19.tar.gz  
cd lighttpd-1.4.19  
sudo ./configure  
sudo make  
sudo make install  
  
ls -la /usr/local/sbin/ # should contain lighttpd (and lighttpd-angel)  
ls -la /usr/local/lib/ # should contain whole bunch of mod_... files  
  
# now since this is bare ass installation,   
# we need to make init scripts and such ourselves  
sudo adduser lighttpd  
  
sudo apt-get install authbind  
cd /etc/authbind/byport/  
sudo touch 80  
sudo chown lighttpd:lighttpd 80  
sudo chmod 775 80  
  
sudo mkdir /etc/lighttpd  
sudo chown lighttpd:lighttpd /etc/lighttpd/  
sudo su lighttpd  
  
mkdir /home/lighttpd/public_html  
pico /home/lighttpd/public_html/index.html  
<html><body>Congrats I'm running!</body><html>  
# Exit the pico  
  
pico /etc/lighttpd/lighttpd.conf  
server.document-root = "/home/lighttpd/public_html"  
server.port = 80  
index-file.names = ( "index.html", "index.htm" )  
include_shell "/etc/lighttpd/create-mime.assign.pl"  
# Exit the pico  
  
pico /etc/lighttpd/create-mime.assign.pl  
#!/usr/bin/perl -w  
use strict;  
open MIMETYPES, "/etc/mime.types" or exit;  
print "mimetype.assign = (n";  
my %extensions;  
while() {  
  chomp;  
  s/#.*//;  
  next if /^w*$/;  
  if(/^([a-z0-9/+-.]+)s+((?:[a-z0-9.+-]+[ ]?)+)$/) {  
    foreach(split / /, $2) {  
      # mime.types can have same extension for different  
      # mime types  
      next if $extensions{$_};  
      $extensions{$_} = 1;  
      print "".$_" => "$1",n";  
    }  
  }  
}  
print ")\n";  
# Exit the pico  
  
/etc/lighttpd/create-mime.assign.pl  
  
# Runs the lighttpd for test ^C to exit  
authbind /usr/local/sbin/lighttpd -f /etc/lighttpd/lighttpd.conf -D  
  
exit # exits the "sudo su lighttpd"  

```