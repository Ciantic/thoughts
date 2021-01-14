---
title: 'WordPress slow? Try adding database indexes'
date: 2018-06-20T04:39:00.002-07:00
oldUrl: "http://ciantic.blogspot.com/2018/06/wordpress-slow-try-adding-database.html"
---

If you are stuck with using WordPress, sometimes smallest things can make a huge difference:  
  
```
ALTER TABLE `wp_postmeta`  
ADD INDEX `meta_key_then_value` (`meta_key`, `meta_value`(100));  
```
  
This is because many plugins and other crap uses a `meta_value` as a store for datetimes etc. That is very slow to sort without.  
  
One page went from loading 27 seconds, to whopping two seconds. Which is still slow, but bearable with cache in front.