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



#FORMS

##Validation

```JavaScript
     /* FORM VALIDATION */
     
     // First hide errors on page load
     $('form .error').hide();
     
     // Define Function to validate email
      function checkEmail(email) { 
          var pattern = /^([a-zA-Z0-9_\.\-\+])+\@(([a-zA-Z0-9\-])+\.)+([a-zA-Z0-9]{2,4})+$/;
          var emailVal = email;
          return pattern.test(emailVal);
      }
    
     // ON FORM SUBMISSION
     $("form input.submit").click(function() {  
      
      // Hide any errors again (In case the form has already created errors).  
       $('.error').hide();

      // Define Variable for validation and to post
      var Firstname = $("input#FirstName").val();
      var LastName = $("input#LastName").val();
      var Email = $("input#Email").val();
      var State = $("select#State").val();
      
          
      // Validate Firstname
      if (Firstname == "") {
        $("input#FirstName").focus();
        $("input#FirstName").next().show();
        return false;
      } 
      
      // Validate LastName
      if (LastName == "") {
        $("input#LastName").focus();
        $("input#LastName").next().show();
        return false;
      } 
      
      //Validate email by running it through the function.
      if (!checkEmail(Email)) {
        $("input#Email").focus();
        $("input#Email").next().show();
        return false;
        }
      
      // Validate State
      if (State == "") {
        $("select#State").focus();
        $("select#State").next().show();
        return false;
      }
    }); 
```   
 
 
#Compass

###Box Sizing
```css
@import "compass/css3"

@include box-sizing(border-box);
```

###Text Shadow
```css
// Uses defaults set before the import above
.has-single-shadow {
  @include single-text-shadow; }
 
// Can output up to ten text shadows
.has-custom-shadow {
  @include text-shadow(rgba(blue, 0.2) 1px 1px 0, rgba(blue, 0.2) 2px 2px 0, rgba(blue, 0.2) 3px 3px 0); }
```

###Box Shadow
```css
 @import "compass/css3";

// Default single box shadow
#box-shadow-default {
 @include single-box-shadow; 
 }

// Box shadow with custom settings
#box-shadow-custom {
 @include box-shadow(red 2px 2px 10px);
 }
 
#box-shadow-custom-multiple
  @include box-shadow(rgba(blue, 0.4) 0 0 25px, rgba(green, 0.2) 0 0 3px 1px inset);
  }
```


###Transitions
```css
#width {
  @include transition-property(width); }
 
#width:hover {
  width: 80px; }
 
#width-duration {
  @include transition-property(width);
  @include transition-duration(2s); }
 
#width-duration:hover {
  width: 80px; }
 
#width-duration-easein {
  @include transition-property(width);
  @include transition-duration(2s);
  @include transition-timing-function(ease-in); }
 
#width-duration-easein:hover {
  width: 80px; }
 
#width-delay {
  @include transition-property(width);
  @include transition-delay(2s); }
 
#width-delay:hover {
  width: 80px }
```
	
#jQuery - No conflict

```javascript

jQuery(document).ready(function( $ ) {

});
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
