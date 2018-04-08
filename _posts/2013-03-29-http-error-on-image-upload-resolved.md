---
title: "HTTP Error on Image Upload [RESOLVED]"
permalink: "http-error-on-image-upload-resolved"
categories:
  - WordPress
  - Error
  - Server
  - nginx
---

This was a fun little issue to come across - I've been using Nginx as my local development server and so far have had few complications, however anytime I went to upload an image I would get a very vague `HTTP Error` from WordPress.

After googling and coming up with everything ranging from disabling plugins to changing your .htaccess file (um, sorry probably not going to help since I'm using Nginx and you know, Nginx doesn't use .htaccess files), I found this <a href="http://wordpress.org/support/topic/http-error-on-image-uploader-1">little gem</a>.

What you want to do is add `client_max_body_size 100m;` to the `http{}` block section of your nginx `.conf` file like so:

```nginx
http {
	client_max_body_size 100m;
}
```

So nice to figure that one out.