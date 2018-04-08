---
title: "Full listing of all WordPress functions"
permalink: "full-listing-of-all-wordpress-functions"
categories:
  - WordPress
  - Programming
  - Script
---

Because I'm a huge nerd and my google search results failed to bring up anything resembling a true listing, I thought I would throw together a little curl, grep and sed magic.

Mostly spent time adjusting the regex to get it just right and strip out all non-essential elements.

```bash
curl -s http://codex.wordpress.org/Function_Reference | grep -C 0 "title=\"Function Reference" | sed 's/.*:.*Function Reference\/.*">//' | sed 's/<.*>//' | sed 's/(.*)//' > wp-functions.txt
```

[Gist](https://gist.github.com/4511254)

<strong>UPDATE:</strong> I was informed by <a title="Ryan Duff, Twitter fiend" href="https://twitter.com/ryancduff">Mr. Ryan Duff</a> there is in fact a much more comprehensive listing over at <a title="much more comprehensive WordPress function listing" href="http://api.wpseek.com/?method=wordpress.getfunctions&amp;output=plain">WP Seek</a>.