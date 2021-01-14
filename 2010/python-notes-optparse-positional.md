---
title: 'Python notes, optparse positional argument parsing'
date: 2010-02-20T10:40:00.000-08:00
oldUrl: "http://ciantic.blogspot.com/2010/02/python-notes-optparse-positional.html"
tags : [python]
---

```python
 parser = optparse.OptionParser()  
    try:  
        (options, (first_posarg, second_posarg, )) = parser.parse_args()  
    except ValueError:  
        parser.error("Two positional arguments are required.")
```