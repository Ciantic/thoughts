---
title: 'ImageMagick: Save for web (JPG)'
date: 2012-10-13T06:41:00.002-07:00
oldUrl: "http://ciantic.blogspot.com/2012/10/imagemagick-save-for-web-jpg.html"
---

Okay this is required in _all web applications_ that allows people to upload images for viewing in browser:  
  
`convert input.jpg -profile AdobeRGB1998.icc -colorspace sRGB -auto-orient output.jpg  `
  
Notice that in above input.jpg need not to be jpg, it can be BMP/PNG... any format that imagemagick reads, it's perfect way to convert anything user uploads to the JPG.  
  
I got a gaping wound as group of users had managed to upload bunch of JPG images with CMYK profiles! As a programmer it would be far easier if there were command like convertweb or something that would just converted any image to PNG or JPG that just works in browsers.