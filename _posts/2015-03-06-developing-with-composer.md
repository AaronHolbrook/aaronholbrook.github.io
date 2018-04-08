---
title: "Developing With Composer"
permalink: "/developing-with-composer/"
categories:
  - Screencast
  - Programming
  - PHP
  - Composer
---

Did you know you can not only use Composer to manage dependencies, but actually develop a package alongside your dependencies?

It's called <a href="https://getcomposer.org/doc/03-cli.md#install">`--prefer-source`</a> and boy is it neat.

The gist of it is this: you define a repository and require the package as you would for a normal dependency, but when you go to run `composer install` or `composer update` you pass the flag `--prefer-source` along with it.

This brings down the entire repo of the package, and provided you have access to commit to that repo, you can easily work inside the package and push changes up just as if you were working within a submodule or <a href="http://www.youtube.com/embed/E7YWeRFHpXg">subtree</a> (an avenue I explored briefly before discovering this method).

I've recorded a fairly short (10 min) screencast of how to include a package from a private github repository, autoload the main file and use `--prefer-source` to be able to make changes directly within the package.

{% include responsive-embed url="https://www.youtube.com/embed/fBJ5_7i06TY" %}
