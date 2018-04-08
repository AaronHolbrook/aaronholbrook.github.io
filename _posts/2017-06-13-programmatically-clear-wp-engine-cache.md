---
title: "Programmatically clear your WP Engine cache"
permalink: "programmatically-clear-wp-engine-cache"
categories:
  - Server
  - WordPress
  - Package
  - Plugin
---

In my desire to create a better process for building and deploying at <a href="http://zeek.com">Zeek</a>, I recently hit a road bump while trying to perform automatic visual regression testing immediately after deployment.

![center-aligned-image](/images/wpengine.png){: .align-center}

This is due to WP Engine's full page cache.

Immediately after we deploy our changes, WP Engine's cache is still showing the old files and has not yet been cleared/flushed/rebuilt. This means our visual acceptance test is testing our <em>pre</em>-deploy changes.

This is entirely unacceptable; this means that we won't know if something is broken until an <em>unknown, later date</em>. In the world of deploying changes, you want to know immediately if the changes you've made had a negative impact, so you can do something about it while you're around, not later when you're out on a walk with your family.

Unfortunately WP Engine currently does not offer a programmatic (i.e. non-manual) solution to this issue.

And so I built one myself: <a href="https://github.com/a7/wpe-cache-flush/">WPE Cache Flush</a>.

I began diving into the code that powers the WP Engine functionality on the site. What I found was the functionality that allows the purge cache button to work.

![center-aligned-image](/images/wpe-purge-cache.png){: .align-center}

I then replicated that functionality in my own package and created a webhook listener.

And now we have a programmatic way to purge the WP Engine cache!

This is both a WordPress plugin as well as a composer package: <strong><a href="https://github.com/a7/wpe-cache-flush/">WPE Cache Flush</a></strong>

Enjoy!