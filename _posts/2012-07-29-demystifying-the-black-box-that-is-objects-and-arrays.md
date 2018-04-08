---
title: "Demystifying the black box that is objects and arrays"
permalink: "demystifying-the-black-box-that-is-objects-and-arrays"
categories:
  - Programming
  - PHP
---

Something I hear all the time and that was initially the biggest learning for me was understanding the data and the structure of objects that we have to interact with.

If you want to become a better programmer, you first need to understand what it is you're trying to manipulate before you can try to manipulate. Imagine trying to solve a Rubik's Cube with a blindfold. That is essentially what you're trying to do without knowing how your data structure is arranged.

Ok - enough with the abstract, let's look at some code.

Something fairly typical I do is to get some meta fields out of the database, so let's use that as an example.

The code to retrieve some <a href="http://codex.wordpress.org/Function_Reference/get_post_meta">post meta</a> is as follows:

```php
get_post_meta($post_id, $key, $single);
```

Let us also imagine that the field we'll be retrieving is not a simple string, it is _gasp_ an array, or even worse - a multidimensional array. I'm going to assume for the moment that you already know what an <a href="http://en.wikipedia.org/wiki/Array_data_structure">array</a> is.

So are field is an array and we need a specific part of that array. If we're just starting to build out our theme and aren't the ones that put the array together, how do we know what's stored in it?

Simple - we use a PHP tool called <a href="http://php.net/manual/en/function.var-dump.php">`var_dump()`</a>. Essentially what this tool does is output the complete array structure for us to examine.

For the purposes of our example, I'll do a var_dump of our retrieved meta value:

```php
$array_variable = get_post_meta('1', 'custom_field_example', true);
var_dump($array_variable); 
```

Result:
```php
array(2) {
  ["key"]=>
  string(5) "value"
  ["key2"]=>
  array(1) {
    ["tax_query"]=>
    string(8) "taxonomy"
  }
}
```

Right off the bat we can see that we have a multidimensional array. Now if we needed to just use an element within that array we could specify just that element. I will do so simply within the var_dump: 

```php
var_dump($array_variable['key2']);
```

Result:
```php
array(1) {
  ["tax_query"]=>
  string(8) "taxonomy"
}
```

The important thing to take away from all this is that `var_dump()` is your friend. Use it to experiment. If you're unsure of what a variable or object contains `var_dump` it!

Understanding that I could explore arrays and objects with `var_dump()` was a major milestone on my path to becoming a better developer.