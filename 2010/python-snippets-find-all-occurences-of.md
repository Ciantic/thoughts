---
title: 'Python snippets, find all occurences of string'
date: 2010-01-02T07:23:00.001-08:00
oldUrl: "http://ciantic.blogspot.com/2010/01/python-snippets-find-all-occurences-of.html"
tags : [python]
---

```
  
>>> def find_all(string, occurrence):  
...     found = 0  
...  
...     while True:  
...         found = string.find(occurrence, found)  
...         if found != -1:  
...             yield found  
...         else:  
...             break  
...  
...         found += 1  
...  
>>>  
>>> print list(find_all("awpropeoaspwtoapwroawpeoaweo", "p"))  
[2, 5, 10, 15, 21]  
>>>  
>>> print list(find_all("Overllllapping", "ll"))  
[4, 5, 6]  

```

**Note**: Finds all _overlapping_ matches.