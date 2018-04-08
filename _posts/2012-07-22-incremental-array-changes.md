---
title: "Incremental Array Changes"
permalink: "incremental-array-changes"
categories:
  - Programming
  - PHP
---

Something that I've come across recently as I start to build dynamic queries is changing the arguments array ever so slightly.

At first I was doing this

If featured posts:

```php
$args = array(
	'post_type'				=> 'charity',
	'order'					=> 'ASC',
	'posts_per_page'		=> -1,
	'showposts'				=> 1,
	'tax_query'				=> array(array(
		'taxonomy'			=> 'charity-category',
		'field'				=> 'slug',
		'terms'				=> 'featured'
	))
);
```

If not featured posts:
```php
$args = array(
	'post_type'				=> 'charity',
	'order'					=> 'ASC',
	'posts_per_page'		=> -1,
	'showposts'				=> 1,
);
```

After being frustrated by the redundancy and trying a couple different variations I discovered the correct way to push elements onto the `$args` array.

This is the correct way to create incremental array changes for your array:

First, declare all common attributes
```php
$args = array(
	'post_type'				=> 'charity',
	'order'					=> 'ASC',
	'posts_per_page'		=> -1,
);
```

If featured posts, declaring incrementally
```php
$args['showposts'] = 1;
$args['tax_query'] = array(array(
		'taxonomy'			=> 'charity-category',
		'field'				=> 'slug',
		'terms'				=> 'featured'
));
```
If not featured posts then we're done!

I thought at first you could simply push the array element (say `tax_query` which is actually an array itself), but that actually puts it at the wrong level in the `$args` array. Let's take a look.

Here's the output from our first full array entry (using <a href="http://php.net/manual/en/function.var-dump.php">var_dump</a>):

```php
array(5) {
  ["post_type"]=>
  string(7) "charity"
  ["order"]=>
  string(3) "ASC"
  ["posts_per_page"]=>
  int(-1)
  ["showposts"]=>
  int(1)
  ["tax_query"]=>
  array(1) {
    [0]=>
    array(3) {
      ["taxonomy"]=>
      string(16) "charity-category"
      ["field"]=>
      string(4) "slug"
      ["terms"]=>
      string(8) "featured"
    }
  }
}
```

Now, if we were to use the <code><a href="http://php.net/manual/en/function.array-push.php">array_push</a></code> method this is what we would get (assuming we're pushing the <code>tax_query</code> array).

```php
array(5) {
  ["post_type"]=>
  string(7) "charity"
  ["order"]=>
  string(3) "ASC"
  ["posts_per_page"]=>
  int(-1)
  ["showposts"]=>
  int(1)
  [0]=>
  array(1) {
    ["tax_query"]=>
    array(1) {
      [0]=>
      array(3) {
        ["taxonomy"]=>
        string(16) "charity-category"
        ["field"]=>
        string(4) "slug"
        ["terms"]=>
        string(8) "featured"
      }
    }
  }
}
```

You can clearly see we're off by a whole level at line 13. So the way around this is to just specify in the `array_push` the element.

```php
$args = array(
'post_type'				=> 'charity',
'order'					=> 'ASC',
'posts_per_page'	=> -1,
'showposts'				=> 1,
);

$args['tax_query'] = array(array(
	'taxonomy'			=> 'charity-category',
	'field'				=> 'slug',
	'terms'				=> 'featured'
));
```

And the output:
```php
array(5) {
  ["post_type"]=>
  string(7) "charity"
  ["order"]=>
  string(3) "ASC"
  ["posts_per_page"]=>
  int(-1)
  ["showposts"]=>
  int(1)
  ["tax_query"]=>
  array(1) {
    [0]=>
    array(3) {
      ["taxonomy"]=>
      string(16) "charity-category"
      ["field"]=>
      string(4) "slug"
      ["terms"]=>
      string(8) "featured"
    }
  }
}
```

As you can see this matches the array structure that we want.

And there you have it! Incremental array changes - helpful when creating a dynamic query!