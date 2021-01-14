---
title: 'Windows 7 - Photo Viewer was really slow'
date: 2011-07-30T07:53:00.000-07:00
oldUrl: "http://ciantic.blogspot.com/2011/07/windows-7-photo-viewer-was-really-slow.html"
tags : [windows7]
---

_Windows 7 Photo Viewer_ was acting really slow for loading images, this fixed it:  
  

1.  Go to _Color management_ (Desktop -> Screen Resolution -> Advanced Settings -> Color Management -> Color Management -> Advanced (tab) -> Change System Defaults)
2.  Remove all profiles from all screens, and add single profile per display. (I chose _sRGB virtual device mode profile.)_
3.  Check the colors in Photo Viewer if the colors are fine then you chose good profile.

  
That did the trick.