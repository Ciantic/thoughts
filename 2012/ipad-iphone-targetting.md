---
title: 'iPad & iPhone targetting'
date: 2012-01-13T02:41:00.000-08:00
oldUrl: "http://ciantic.blogspot.com/2012/01/ipad-iphone-targetting.html"
---

```css
/* iPad [portrait + landscape] */  
@media only screen and (min-device-width: 768px) and (max-device-width: 1024px) {  
 .selector-01 { margin: 10px; }  
 .selector-02 { margin: 10px; }  
 .selector-03 { margin: 10px; }  
}  
  
/* iPhone [portrait + landscape] */  
@media only screen and (max-device-width: 480px) {  
 .selector-01 { margin: 10px; }  
 .selector-02 { margin: 10px; }  
 .selector-03 { margin: 10px; }  
}  
  
/* == iPad/iPhone [portrait + landscape] == */  
@media only screen and (min-device-width: 768px) and (max-device-width: 1024px),   
@media only screen and (max-device-width: 480px) {  
 .selector-01 { margin: 10px; }  
 .selector-02 { margin: 10px; }  
 .selector-03 { margin: 10px; }  
}  

```Stolen from [Preishablepress](http://perishablepress.com/press/2010/10/20/target-iphone-and-ipad-with-css3-media-queries/)