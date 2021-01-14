---
title: 'Python notes, halving list'
date: 2009-03-26T10:59:00.000-07:00
oldUrl: "http://ciantic.blogspot.com/2009/03/python-notes.html"
tags : [python]
---

**Splitting list from the middle:**  

```
>>> a = [34,412,3,2,4,6,78,9,2]  
>>> [a.pop(0) for alk in a]  
[34, 412, 3, 2, 4]  

```... tricky ain't it.