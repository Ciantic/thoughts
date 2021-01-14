---
title: 'Sticky Footer & Variable Height - modern CSS'
date: 2011-10-21T11:07:00.000-07:00
oldUrl: "http://ciantic.blogspot.com/2011/10/sticky-footer-variable-height-modern.html"
tags : [css, html]
---

**Copy & Pasted** from [http://pixelsvsbytes.com/blog/2011/09/sticky-footers-the-flexible-way/](http://pixelsvsbytes.com/blog/2011/09/sticky-footers-the-flexible-way/) Page was down for me, so salvaged this from Bing search cache (Google cache didn't have):  

  

\-- cut --  

> **Step 3:** All we have to do now is to put our CSS and HTML code together. Fortunately we can use the `body` element as .Frame, so there is no need for an extra `div` tag or so.
> 
> ```
> <!DOCTYPE HTML>  
> <html>  
> <head>  
>     <style type="text/css">  
>         html, body {  
>              height: 100%;  
>              margin: 0pt;  
>         }  
>         .Frame {  
>              display: table;  
>              height: 100%;  
>              width: 100%;  
>         }  
>         .Row {  
>              display: table-row;  
>         }  
>         .Row.Expand {  
>              height: 100%;  
>         }  
>     </style>  
> </head>  
> <body class="Frame">  
>     <header class="Row"><h1>Catchy header</h1></header>  
>     <section class="Row Expand"><h2>Awesome content</h2></section>  
>     <footer class="Row"><h3>Sticky footer</h3></footer>  
> </body>  
> </html>
> ```
> 
> **Note:** Remember to include the [html5shiv](http://code.google.com/p/html5shiv/) workaround in your page (and define appropriate CSS styles) if you want to use HTML5 tags in IE8 and below. Or simply use `div` tags instead of `header`, `section` and `footer`.
> 
> A word on older browsers
> ========================
> 
> The code above will work even with older versions of Firefox, Opera and Safari, so there is nothing to worry about here, but unfortunately Internet Explorer 7 and below don’t know anything about `display:table` or `display:table-row`, so we go the way of graceful degradation here.
> 
> The first thing we have to to is, to prevent the margins of elements inside the row from being outside of it, by adding `overflow:hidden` to the `.Row` style.
> 
> That gives us quite acceptable results, but the footer will always be outside of the window due to the 100% height of the `.Frame` and the `.Row`. The solution is to set `height:100%` in a way that all Internet Explorer versions below 8 won’t recognize. I’m using the (valid) `html>/**/body` CSS hack to accomplish this, but you might also use conditional comments if you feel better that way. However, here is the fixed CSS:
> 
> ```
> .Frame {  
>     display: table;  
>     width: 100%;  
> }  
> html>/**/body .Frame {  
>     height: 100%;  
> }  
> .Row {  
>     display: table-row;  
>     overflow: hidden;  
> }  
> html>/**/body .Row.Expand {  
>     height: 100%;  
> }
> ```
> 
> I guess it shouldn’t be too complicated to create a sticky footer by adjusting the height of `.Row.Expand` with some little Javascript.

\-- paste --