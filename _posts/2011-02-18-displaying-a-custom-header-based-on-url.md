---
title: "Displaying a custom header based on URL"
permalink: "/displaying-a-custom-header-based-on-url/"
categories:
  - WordPress
  - Programming
---
So I recently ran across a situation on Centegra's website where I had set up our header image to show an image based on the section or area it's in. This was working fine utilizing a custom `get_ID_by_slug('slug-of-post')` function I built to get the post ID.

The problem with using custom post types though, is that if you're displaying an archive listing of the custom post types, you're unfortunately not able to just test whether or not the loop you're in is a custom post type (since you're listing them, you're one level above).

My current solution I discovered was to test for the permalink or URL. This will only work if you have your permalink structure set up to show `/%post-name%/` and if you're using the Simple Custom Post Type plugin which displays lists of custom post types for you (WordPress unfortunately still has not added this functionality at the time of this posting).

I store the URL in a variable, the string I want to test for (in this case the location custom post type listing) and then use the PHP function strpos (which will return positive if the second string is contained within the first string).

Here's the code for those interested:

```php
$server_uri = $_SERVER['REQUEST_URI'];
$spt_location = "location/";
else if ( $wp-<query_vars["post_type"] == "locations" || strpos($server_uri,$spt_location)  ) { ?>
<img src="&lt;?php bloginfo('stylesheet_directory'); ?&gt; image location here " alt="" /> <?php } ?>
```