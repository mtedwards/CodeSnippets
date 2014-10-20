CodeSnippets
============

CodeSnippets that I refer to a lot:

#WordPress

###Passing a variable through the content filter

```php
  <?php 
    $something = apply_filters('the_content', $something);
    echo $something;
  ?>
```

###Retrieve and display a Video URL

```php
  <?php 
    $song = get_field('song_link'); 
    $song = preg_replace('/\s+/', '', $song);	
    $song = wp_oembed_get($song);
    echo $song;
  ?>
```
###Featured Images
The post thumbnail
```php
<?php
  if ( has_post_thumbnail() ) {
    the_post_thumbnail('thumbnail', array('class' => 'alignleft'));
  }
?>
```

Get Custom Size
```php
<?php
  if ( has_post_thumbnail() ) {
    $url = wp_get_attachment_image_src( get_post_thumbnail_id($post->ID), 'CUSTOM SIZE');
  }
?>
```


Add Image Size
```php
if ( function_exists( 'add_image_size' ) ) { 
	add_image_size( 'category-thumb', 300, 9999 ); //300 pixels wide (and unlimited height)
	add_image_size( 'homepage-thumb', 220, 180, true ); //(cropped)
}
```


##The Loop

###Query by Custom Field
```php
  <?php
    $args = array(
      'post_type' => array(
        'your-post-type',
      ),
      'order' => 'ASC',           
      'orderby' => 'menu_order',
      'meta_key' => 'your-custom-field',
      'meta_value' => 'your-custom-field-value'
    );
    
    $the_query = new WP_Query( $args );
    // The Loop
    
    if ( $the_query->have_posts() ) :
      while ( $the_query->have_posts() ) : $the_query->the_post(); 
  ?>
  
  THE STUFF THAT HAPPENS
  
  <?php
      endwhile;
    endif;
    
    // Reset Post Data
    wp_reset_postdata();
  ?>
```

#Foundation

##Settings

```css
// Using rem-calc for the below breakpoint causes issues with top bar
   $topbar-breakpoint: 810px; // Change to 9999px for always mobile layout
   $topbar-media-query:"only screen and (min-width: #{$topbar-breakpoint})" !default;
```

	
###jQuery - No conflict

```javascript

jQuery(document).ready(function( $ ) {

});
```
###ID Exist

```javascript
if($("#tagLineCanvas").length){
  tagLine();
}
```


#OTHER Code

###Redirect to other site, with pause for Analytics

####Don't forget came from code!!

```php

 <?php 
   /*
     Template Name: PUT THE TEMPLATE NAME
   */
 ?>
 
  <head>
  <title>TITLE FOR GOOGLE ANALYTICS</title>
	 <script type="text/javascript">
   
   // Google Analytics - Check this is the right one for the site
  	 
    var _gaq = _gaq || [];
    _gaq.push(['_setAccount', 'XXXXXXX']);
    _gaq.push(['_trackPageview']);
  
    (function() {
      var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
      ga.src = ('https:' == document.location.protocol ? 'https://' : 'http://') + 'stats.g.doubleclick.net/dc.js';
      var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
    })();
    
    // Facebook Remarketing???

      
      // Google Remarketing??
      
    
    setTimeout(function () {
      window.location = "ADD THE ADDRESS HERE!!!!";
    }, 200);
  </script>
  </head>
  
```


## Foundation Map Styles

```css
 #map-canvas *, #map-canvas *:before, #map-canvas *:after {
        -moz-box-sizing: content-box!important;
        -webkit-box-sizing: content-box!important;
        box-sizing: content-box!important;  
    }
    #map-canvas img {
        max-width: none;
    }
    #map-canvas label {
        width: auto;
        display: inline;
    }
 ```
