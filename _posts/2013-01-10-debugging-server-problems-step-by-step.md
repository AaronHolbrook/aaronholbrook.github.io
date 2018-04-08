---
title: "Debugging server problems step by step"
permalink: "/debugging-server-problems-step-by-step/"
categories:
  - Server
  - Linux
  - Programming
---

First off, I have to give major thanks to <a title="WordPress Badass" href="http://evansolomon.me/">Mr. Evan Solomon</a> for very graciously helping me diagnose and fix a very hard to pinpoint bug with NGINX and WooCommerce.

I had recently moved a customized WooCommerce site from MediaTemple GS (which runs Apache as its webserver) to a custom built Linode VPS (which I am running NGINX on). The Linode VPS was successfully set up with NGINX, APC and Varnish cache. The site worked fine, PHP loaded fine, WordPress worked and ran fine. I even had pretty permalinks working just fine with NGINX. So far so good right?

So I thought - until my client noticed she could not add any of the products to the cart. Quite odd since I didn't actually change anything in the code, I had simply migrated the files and database to the new server.

I started to snoop around and I hypothesized that perhaps some of the heavy caching was the culprit. So I disabled Varnish and APC. Still the problem persisted. (This is about the time I brought Evan in).

Evan suggested I look through the WooCommerce function, most notably the part that validates what has been added to the cart. I refused to believe anything could be wrong in the code, especially because I hadn't changed anything! It had to be a server issue, right?

Turns out, going through the code is VERY beneficial, because you can pinpoint at what point the problem is occurring. I placed a `var_dump($_REQUEST)`, starting just at the point the WooCommerce validation runs. It came back as `NULL`.

Huh. So - why wouldn't it be receiving the query parameters? Ok - let's go further up suggested Evan. Let's place a `var_dump` in `wp-blog-header.php`. I did and it turned out that `$_REQUEST` was still `NULL`.

I even put it in `index.php` - it couldn't possibly be `NULL` here right? Yep - definitely `NULL`.

Ok - let's try a simple file called `request.php` and put inside it the following.

```php
var_dump($_REQUEST);
```

Let's visit that then with a query string: site/request.php?foo=bar.

Result worked great, so what was it about `index.php` that had us so stumped?

Ready for this?

Turns out the problem was in the NGINX server config file! In the area for `try_files`, I had the following:

```nginx
location / {
  try_files $uri $uri/ /index.php;
}
```

Unfortunately, the end result of this is that it strips all query parameters at the end of `index.php`.

Evan helped me realize that the configuration should instead look like this:

```nginx
location / {
  try_files $uri $uri/ /index.php?$args;
}
```

Don't forget to restart or reload nginx after you've made any changes to the config files!

```bash
sudo service nginx reload
```

So - even if you know the code is good, it helps to debug thoroughly to identify where the problem resides.

Thanks Evan for your help! You're a rockstar!