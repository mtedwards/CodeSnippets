CodeSnippets
============

CodeSnippets that I refer to a lot:

##WordPress

###Passing a variable through the content filter


```php
  <?php 
    $something = apply_filters('the_content', $something);
    echo $something; ?>
```
