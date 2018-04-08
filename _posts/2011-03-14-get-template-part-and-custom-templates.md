---
title: "get_template_part and Custom Templates"
permalink: "get_template_part-and-custom-templates"
categories:
  - WordPress
  - Programming
---

In building the Centegra physician directory back in WordPress 3.0, there was no real way to use WordPress to display out a listing or archive of your custom posts. The temporary workaround solution was a little plugin I found called <a href="http://www.cmurrayconsulting.com/software/wordpress-custom-post-type-archives/">'<strong>Simple Custom Post Type Archives</strong></a>'. It worked well and all I had to do was create a file in the theme's directory in the format type-custompostslug.php.

However in 3.1 they've included much better support for utilizing the already built archives to display a listing of your custom posts.

It took me a little bit of work and digging into using the oh-so-fun get_template_part function, but I believe I've uncovered the right way (at least for me, for the time being).
<h2>Step 1</h2>
You will be using archive.php, so make sure you're familiar with it. (If you haven't used it before you should definitely take a <a href="http://codex.wordpress.org/Creating_an_Archive_Index">look</a>)

In your archive.php, use an if statement to determine what you're outputting, if you're outputting your custom post type then take action. (Place above the last else clause)

```php
if ( get_post_type($post) == 'physicians') {
```

In this case, I'm actually displaying a search form if they land on the physicians page, so this becomes one step more complex - I now have to work in the search.php file.

<h2>Step 2 and get_template_part()</h2>

Originally, I thought the two parts of get_template_part ( 'loop', 'search') called the loop.php file then went to a sub-section called search. Actually what happens is it first looks for whatever you list in the first spot (in this case loop). The second area is actually if you'd like to specify a different file - if it exists (loop-search.php) than it calls that, if not it just calls loop.php.

This is insurmountably useful to keep your site logic separate. In this case I want to keep the physician listing separate from the default archive listing.

So I call it:


```php
if ( $_GET['post_type'] == 'physicians') {
  get_template_part( 'loop', 'physician-search-results' );
}
```

Put that above the original `get_template_part( 'loop', 'search')` and turn that into an else statement.

Make your modifications to however you want to display your custom post and you're done!