---
title: "Auto-update version of css"
permalink: "auto-update-version-of-css"
categories:
  - WordPress
  - Programming
---

I just stumbled across this on [Mark Jaquith's blog](http://markjaquith.wordpress.com/).

It's a really handy way of getting around the automatic caching that happens to css files.

```php
<link rel="stylesheet" href="<?php bloginfo('stylesheet_url'); echo '?' . filemtime( get_stylesheet_directory() . '/style.css'); ?>" type="text/css" media="screen, projection"
```

Basically it uses the timestamp as the variable that changes. Anytime you update the css file any browser will think it's a new file and go and get it.

Simple and useful - thanks Mark!

via: <a href="http://markjaquith.wordpress.com/2009/05/04/force-css-changes-to-go-live-immediately/">http://markjaquith.wordpress.com/2009/05/04/force-css-changes-to-go-live-immediately/</a>