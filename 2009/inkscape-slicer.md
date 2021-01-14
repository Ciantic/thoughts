---
title: 'Inkscape slicer'
date: 2009-02-21T18:02:00.000-08:00
oldUrl: "http://ciantic.blogspot.com/2009/02/inkscape-slicer.html"
tags : [inkscape, webdesign]
---

[Download Inkscape slice effect a.k.a. 'slicer' 0.1.1 (bugfix)](http://users.jyu.fi/%7Ejaotospe/inkscape/slicer/slicer0.1.1.tar.gz)

## Usage:

1. Create layer e.g. named 'slices'.  
2. Create rectangles as your slices, set their Label\* (select rect and Object -> Object properties) as the output filename (without extension).  
3. Run Effects -> Export -> Slicer, specify directory where you want your slices to be saved and Apply.  
  

## What program does:

1. It takes all rectangles you give, puts opacity 0, stroke to none.  
2. And tries to save contents inside rectangles to new files.  
3. Returns the style to original value.  
  

## Installation:

Copy these two files (slicer.py, slicer.inx) to share/extensions directory inside inkscape, do not create directory for these files.  
  
Extensions dir in common platforms:  
Ubuntu 8.10 user scope: ~/.inkscape/extensions/  
Ubuntu 8.10 global scope: /usr/share/inkscape/extensions/  
Windows: c:\\Program Files\\Inkscape\\share\\extensions\\  
  

## Thanks

Original idea from [Matt Harrison](http://panela.blog-city.com/slicing_web_pages_with_inkscape_and_python.htm):  
WARNING, Matt's version didn't work with latest Ubuntu (8.10) and Inkscape 0.46, major API differences, that was the reason I rewrote whole script with features I needed. I have no intention to ripoff Matt's effort, so I fully thank Matt for his work, and if you somehow feel that I have broken the license in Matt's file you can contact me through comments in this blog.  
  
*** 

Label allows all characters, where as ID allows only few. I need ability to use spaces in filenames so ID is no go. One can switch it to back to ID by changing line in slicer.py:  
`basename = rect_label.lstrip("#")`  
to  
`basename = rect_id`