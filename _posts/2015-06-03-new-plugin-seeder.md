---
title: "New plugin: Seeder"
permalink: "new-plugin-seeder"
categories:
  - WordPress
  - Plugin
---

It's nice to pre-populate terms, content or have the ability to only OCCASIONALLY run actions.

In the past, I've had to manually use special `$_GET` variables.

Not any more! Newly released today is a little library I'm calling Seeder. What it does is provide a simple interface for admins/super admins to fire a special hook. You can easily hook onto that action in order to perform your infrequent or expensive logic.

This could be anything such as pre-filling content, auto-creating terms, updating the database in a certain manner, talking to or updating an API, etc.

Check it out on <a href="https://github.com/AaronHolbrook/seeder">github</a> or <a href="https://packagist.org/packages/aaronholbrook/seeder">packagist</a>.

Extra special thanks to <a href="http://joshlevinson.me/">@joshnlevinson</a> for his work on building the beginning of this and for coining the term of seeding. Thanks Josh!