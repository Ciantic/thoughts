---
title: 'Aero Snap vertical maximize winapi'
date: 2010-06-22T02:41:00.000-07:00
oldUrl: "http://ciantic.blogspot.com/2010/06/aero-snap-vertical-maximize-winapi.html"
tags : [windows7, winapi]
---

Easy way to toggle the Aero Snap vertical maximize in WinAPI:  
```C
HWND active = GetForegroundWindow();  
PostMessage((HWND) active, WM_NCLBUTTONDBLCLK, HTTOP, 0);  
```