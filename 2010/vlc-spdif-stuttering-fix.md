---
title: 'VLC S/PDIF Stuttering fix'
date: 2010-02-06T14:16:00.000-08:00
oldUrl: "http://ciantic.blogspot.com/2010/02/vlc-spdif-stuttering-fix.html"
---

I had this problem with VLC where all output going S/PDIF was stuttering with Windows Vista, and now that I got myself Windows 7 X64, I had to re-fix this problem.  

Now I finally found the fix, so I decided to save it to here for future reference:  

Preferences -> Advanced settings -> Audio -> Output modules -> Win32 waveOut extension output.  

![](./vlc-spdif-stuttering-fix-01.png)

Now the AC3/DTS passthrough works without stuttering.