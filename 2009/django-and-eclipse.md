---
title: 'Django and Eclipse'
date: 2009-02-12T16:11:00.000-08:00
oldUrl: "http://ciantic.blogspot.com/2009/02/django-and-eclipse.html"
tags : [eclipse, pydev, django, python]
---

(When I have interest, I have planned to convert this to HTML, for now, let it be Plain text)  
Anyone is welcome to edit, repost and/or distribute the following instructions, I just have a little wish: Provide link for this post.  
```
  
Used: Eclipse Classic Ganymede (3.4.1), Django 1.0.2, PyDev  
  
Install Pydev  
=============  
... TODO ...  
  
Python interpreters (Eclipse preferences -> Pydev -> Interpreter - Python)  
--------------------------------------------------------------------------  
Press `New`  
 Type (Ubuntu) `/usr/bin/python`  
 Type (Windows) `C:\Python25\python.exe` *** Warning: not tested!  
 Press `Ok`  
  *IMPORTANT!*  
  If you have installed Django to site-packages  
   *UNCHECK* I repeat *UN*CHECK the Django from the Pythonpath list  
   (Or remove from the list)  
  (We are *NOT* going to use the site-packages django to this for development purposes)  
  
Django project for Eclipse  
==========================  
  
File -> New -> Pydev project  
 Project name: `Django`  
 Grammar version: `2.5`  
 Uncheck `Create default `src` folder and add it to the pythonpath?`  
  Error about interpreter?: `Click here to configure an interpreter not listed` see above Install Pydev section  
  
  
Pydev Package Explorer (the "file tree" on the left) -> Django (right click) -> Properties  
 PyDev - PYTHONPATH  
  Add source folder -> Choose `Django` (the project's "root" directory, for why, see (*1))  
  
(Ubuntu) in terminal (go to your eclipse workspace directory):  
 cd Django/  
 svn co http://code.djangoproject.com/svn/django/tags/releases/1.0.2/ .  
  
(Windows) Extract the django release to the Django/ dir:  
 (after extraction you should have directories like `Django/django`, `Django/examples`, `Django/docs` ...)  
  
Pydev Package Explorer (the "file tree" on the left) -> Django (right click) -> Refresh (now zip some coffee, this might take while)  
  
All is set for Django project.  
  
(*1) Why root? Because for instance `django` and `examples` directories in django distribution should be in pythonpath and they are in root, this is only reasonable way since we won't relocate them.  
  
  
My django project:  
==================  
  
VERY IMPORTANT! DO THE DAMN `Django project for Eclipse` section FIRST! SINCE YOU WON'T GET THE AUTOCOMPLETE/*PLUGGABLE DJANGO VERSION BETWEEN APPLICATIONS* WITHOUT IT.  
  
File -> New -> Pydev project  
 Project name: `Django Poll`  
 Grammar version: `2.5`  
 *Check* I repeat *Check* (It should be checked by default) the `Create default `src` folder and add it to the pythonpath?`  
  Error about interpreter?: This can't be, you set it up on `Django project for Eclipse`  
 Click `Next`  
  (In reference page)  
  Check `Django` (the Django project you created earlier, remember that?)  
  Press `Finish`  
  
Django-admin.py from within Eclipse:  
------------------------------------  
  
Run -> External tools -> External tools configurations  
 Left side tree: Right click `Program` -> New  
  Name: `Django-admin (for project src directory)`  
  Location (Ubuntu): `/bin/bash`  
  Location (Windows): `c:\Windows\system32\cmd.exe`   *** Warning: Not tested  
  Working directory: `${project_loc}/src`  
  
 Environment tab:  
  New (from right)  
   Name: `PATH`  
   Value (Ubuntu): `${env_var:PATH}:${workspace_loc:Django/django/bin}`  
   Value (Windows): `${env_var:PATH};${workspace_loc:Django/django/bin}`   *** Warning: Not tested  
   Click `Ok`  
  New (from right)  
   Name: `PYTHONPATH`  
   Value (Ubuntu): `${project_loc}/src:${workspace_loc:Django/}`  
   Value (Windows): `${project_loc}/src;${workspace_loc:Django/}`   *** Warning: Not tested  
   Click `Ok`  
  
  Press `Apply` and `Close` (Don't try to Run, it will (most likely) give error)  
  
Run -> External tools -> Organize favorites  
 Click `Add`  
  Choose `Django-admin (for project src directory)`  
  Click `Ok`  
 Click `Ok`  
  
Now in order to run this tool one must do *TWO* things:  
  
1.) Pydev Package Explorer (the "file tree" on the left) -> Click on the `Django Poll` project (even if it is selected, just click it (to get focus on it))  
  
2.) Run -> External tools -> `Django-admin (for project src directory)`  
 *** If you get error about `Variable references empty selection: ${project_loc}`, you didn't do 1.) well enough, you *MUST* click it first and nothing else afterwards, the *project folder* in *Pydev Package Explorer* must have *focus* (being selected is not enough)!  
  
 Console window (if not visible do Window -> Show view -> Console), type:   
  `django-admin.py`  
  
 If all went well you should get something like: `Type django-admin.py help for usage.`  
   
 Following is from official django tutorial http://docs.djangoproject.com/en/dev/intro/tutorial01/#intro-tutorial01  
  
 Console window, type:   
  `django-admin.py startproject mysite`  
  
PyDev Package Explorer (the tree on the left) -> `Django Poll` (right click) -> Refresh  
(If all worked well you should now have directory `src/mysite` in your project)  
  
Manage.py from within Eclipse  
-----------------------------  
  
PyDev package explorer (tree in the left) -> `Django Poll` (your project name) -> src -> manage.py (right click) -> Properties  
 (You should be in dialog called `Properties for manage.py`)  
 Click `New...`  
  Choose `Python Run`  
   (For reason unknown Eclipse doesn't prepopulate the following fields)  
   Name: `Django Poll -- Custom manage.py`  (Yes you read it right, I prefixed it with project name for extra verbosity)  
  
   Main tab (default tab):  
    Project click `Browse`, choose your project `Django Poll`  
    Main module click `Browse`, choose `src -> mysite -> manage.py`, click `Ok` (it should now read ${workspace_loc:Django Poll/src/mysite/manage.py} )  
  
   Arguments tab:  
    Press `Variables` (from Program arguments)  
     Choose `string_prompt`  
     (It should have added this `${string_prompt}`)  
     Click `Ok`  
   Click `Ok`  
 Click `Ok`  
  
  
Running test:  
  
Locate Run button from toolbar (Green play button, with arrow downwards next to it), press the arrow -> Choose `Organize Favorites`  
 Press `Add...`  
  Check the `Django Poll: Custom manage.py`  
  
Run button (press the arrow) -> `Django Poll -- Custom manage.py`  
 (If all went well, you should be given prompt)  
 Type: `help`  
  (If all worked well, you should get long list of commands, beginning:  
  
  `Type 'manage.py help <subcommand>' for help on a specific subcommand.`  
  ...)  
  
  
Lets create app:  
  
Run button press the arrow -> `Django Poll -- Custom manage.py`  
 Type: `startapp polls`  
  
Now refresh your project directory from Pydev Package explorer (the tree in the left)  
(If all worked well you should now have directory `src/mysite/polls` in your project)  
  
  
Running the development server  
------------------------------  
Run button (press the arrow) -> `Django Poll -- Custom manage.py`  
 Type: `runserver --noreload`  
  
(You can use it without `--noreload`, but the console window is rather useless in that case, since Eclipse can't handle the refresh behaviour of `manage.py`.)  
  
  
Other Eclipse preferences (optional), though highly recommended  
===============================================================  
  
More run configurations  
-----------------------  
Since you most likely need manage.py's commands `runserver`, `syncdb`, `reset` the most, create own run configurations for those, using similar steps as in "Manage.py from within Eclipse" section.  
  
  
Tasks of project  
----------------  
  
Window -> Show view -> Tasks  
  
Tasks (little `downward triangle` before minimize of tasks window) -> Configure contents  
 Right side of the window: check `On any element in same project`  
 Left side of the window: check `TODOs`  
  
  

```