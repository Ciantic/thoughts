---
title: 'SFTP umask'
date: 2009-01-23T18:13:00.000-08:00
oldUrl: "http://ciantic.blogspot.com/2009/01/sftp-umask.html"
---

Do this `pico /opt/sftp-server.sh`  

```
#!/bin/bash  
# This is a wrapper around the sftp-server subsystem to set umask. Point  
# the subsystem in /etc/ssh/sshd_config to this file. (Ubuntu/Debian  
# file locations assumed)  
  
umask 0002  
exec /usr/lib/openssh/sftp-server
```
  
Remember to `chmod ugo+x /opt/sftp-server.sh`  
  
Then `pico /etc/ssh/sshd_config`  
  
Replace/edit this part:  

```
# Subsystem sftp /usr/lib/openssh/sftp-server # replaced with below  
Subsystem sftp /opt/sftp-server.sh  
```
  
Finally remember: `/etc/init.d/ssh restart`