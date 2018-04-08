---
title: "WordPress Permissions Update Error [RESOLVED]"
permalink: "/wordpress-permissions-update-error-resolved/"
categories:
  - WordPress
  - Server
---

Recently I ran into an issue where an installation of WordPress that had never had any issues updating stopped being able to update via the admin update button.

Specifically these were the errors I would see:

<pre>
Unpacking the update...

The update cannot be installed because we will be unable to copy some files. This is usually due to inconsistent file permissions.: wp-admin/includes/update-core.php

Installation Failed

An automated WordPress update has failed to complete</pre>

The solution as it turns out is to reset the file permissions on the core files.

Provided you have SSH access to your server, the following commands may fix your issue.

Reset the permissions of all files to `664`:

```bash
find /path/to/site/ -type f -exec chmod 664 {} \;
```

Reset permissions of directories to `775`:

```bash
find /path/to/site/ -type d -exec chmod 775 {} \;
```

Reset the group to the `wordpress` group (or whatever group makes sense for you)

```bash
chgrp -R wordpress /path/to/site/
```

After running those commands I was able to successfully update WordPress with no further issues.