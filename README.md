CodeSnippets
============

CodeSnippets that I refer to a lot:

#WordPress

###Passing a variable through the content filter

```php
  <?php 
    $something = apply_filters('the_content', $something);
    echo $something; ?>
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


##The Loop

###Query by Custom Field
```php
    	<?php
		    $args = array( 
		        'post_type' => array(                   
		                'you-post-type',                 
		                ),  
		        'order' => 'ASC',                   
		        'orderby' => 'menu_order',
		        'meta_key' => 'your-custom-field',
		        'meta_value' => 'your-custom-field-value');
		    
		    $the_query = new WP_Query( $args );
		    
		    // The Loop
		    if ( $the_query->have_posts() ) :
		    while ( $the_query->have_posts() ) : $the_query->the_post(); ?>
        
        THE STUFF THAT HAPPENS
        
        <?php
  	    endwhile;
		    endif;
		    
		    // Reset Post Data
		    wp_reset_postdata();
		    ?>

```
