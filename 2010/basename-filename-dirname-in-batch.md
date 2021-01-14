---
title: 'Basename, Filename, Dirname in Batch'
date: 2010-10-21T12:59:00.000-07:00
oldUrl: "http://ciantic.blogspot.com/2010/10/basename-filename-dirname-in-batch.html"
tags : [batch, windows]
---

Umm, batch scripts sucks, but here goes:  
  
```batch
set filepath="C:\\some path\\having spaces.txt"  
  
for /F "delims=" %%i in (%filepath%) do set dirname="%%~dpi"   
for /F "delims=" %%i in (%filepath%) do set filename="%%~nxi"  
for /F "delims=" %%i in (%filepath%) do set basename="%%~ni"  
  
echo %dirname%  
echo %filename%  
echo %basename%  

```  
I have awed this for crap many times before, now I have it here for the future.