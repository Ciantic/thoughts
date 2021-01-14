---
title: 'WP: Turn Off Comments / Ping Backs by Default from Pages'
date: 2011-09-27T09:43:00.000-07:00
oldUrl: "http://ciantic.blogspot.com/2011/09/wp-turn-off-comments-ping-backs-by.html"
tags : [wordpress]
---

Turn Off Comments / Ping Backs by Default from Pages  
  
Themes **functions.php** or **yourplugin.php**:  
  
```php
// This is valid hack as long as "wp-admin/includes/post.php"  
// `get_default_post_to_edit()` keeps calling `apply_filter()` for   
// `default_content` *after* `comment_status` and `ping_status` setting.
function my_disable_pages_default_commenting($content, $post) {  
    if ($post->post_type == 'page') {  
        $post->comment_status = "closed";  
        $post->ping_status = "closed";  
    }  
  
    return $content;  
}  
add_filter('default_content', 'my_disable_pages_default_commenting', 1, 2);
```  
Snippet above turns off the check boxes only from _New Pages_, any existing pages must be unchecked manually.