---
title: 'Duplicate All Pages (in-place) in Acrobat X'
date: 2011-09-23T05:37:00.000-07:00
oldUrl: "http://ciantic.blogspot.com/2011/09/duplicate-all-pages-in-acrobat-x.html"
---

This is just a small JavaScript extension to _Acrobat X_ that allowes to Duplicate all pages _in-place_ there exists another version which used extractPages and I didn't like that behavior so I wrote own.  
  
First _elevate privileges_ of the JavaScript programs:  

1.  Right click on document, and choose "Page Display Preferences"
2.  Choose "JavaScript" from the left.
3.  Check the "Enable menu items JavaScript execution privileges".

Secondly save following snippet as **duplicate.js** to the `%appdata%\Adobe\Acrobat\10.0\JavaScripts` folder:  
```javascript
app.addMenuItem({  
        cExec: "duplicatePagesInPlace();",  
        cParent: "Edit",  
        cName: "Duplicate all pages (in-place)"  
});  
  
function duplicatePagesInPlace() {  
    var doc = this,  
        pages = this.numPages;  
    for (var i = pages - 1; i >= 0; i--) {  
        doc.insertPages({   
            cPath: doc.path,   
            nStart : i,   
            nEnd : i,  
            nPage : i  
        });  
    }  
}  

```  
Now you should be able to access the "Duplicate all pages (in-place)" under "Edit" menu item. If you can't see the item remember to restart Acrobat.