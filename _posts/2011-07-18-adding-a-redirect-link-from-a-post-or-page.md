---
title: "Adding a redirect link from a post (or page)"
permalink: "/adding-a-redirect-link-from-a-post-or-page/"
categories:
  - WordPress
  - Programming
---

I just had a client request that for his home page posts that were being displayed, have them link instead to a permanent page. The type of content that they were linking to was longer term and the posts that were being displayed were created just as excerpts.

Not a problem! Let's just set up a custom field value, call it 'redirect' and go to work.

So we'll be editing the page-home.php file and first testing to see if the custom field value exists.

Using our get_custom_field_value function we'll do a quick if then statement:

```php
<?php if(get_custom_field_value('redirect')) { ?>
<a href="<?php echo get_custom_field_value('redirect'); ?>">
<?php } else { ?>
<a href="<?php the_permalink(); ?>">
<?php } 
the_title(); ?></a></h3>
````

So that will change the title link if there's a redirect value. We can easily add this to the thumbnail so if there's a featured image it'll go to the right page.

```php
<?php if(get_custom_field_value('redirect')) { ?>
<a href="<?php echo get_custom_field_value('redirect'); ?>">
<?php } else { ?>
<a href="<?php the_permalink(); ?>">
<?php } ?>
<?php the_post_thumbnail( 'thumbnail', array('class' => 'thumbnail rounded-img')); ?></a>
```

All in all, fairly quick and easy. Sure there's plugins out there, but using a custom field is a little less taxing and just as easy.