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

```css
@import "compass/css3"

@include box-sizing(border-box);
```
