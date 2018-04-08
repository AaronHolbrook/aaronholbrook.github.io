---
title: "Testing a Transient Locking Mechanism with Siege"
permalink: "testing-transient-locking-mechanism-siege"
categories:
  - WordPress
  - Programming
  - Caching
---

When working with caching strategies, it's important to step through your invalidation strategies. Namely, thinking through at what point does the data that you're caching get regenerated, how does it get regenerated and <em>who</em> is regenerating it. It could be regenerated any time a new post is published, on a `save_post` hook by an author or admin OR it might need to be regenerated every 15 minutes by anyone hitting the front page.

In the latter case, you want to ensure that at the point where the cache has suddenly expired, you're not allowing a number of concurrent users to simultaneously make the call for a regeneration of data (which generally is either computationally expensive, is lengthy or both). One way in which we can limit how many people are all slamming the regeneration is to create a short term transient lock. Essentially the idea is, the first user to go through the conditional statement will set a transient lock behind them and will be the only ones to (in my case) make the call to a weather API.

I wasn't quite sure if this would be effective or not and so I decided to test my theory using <a href="http://www.joedog.org/siege-home/">Siege</a>, a http load testing and benchmarking utility. If you've never used or heard of Siege before, definitely check it out. It's an amazing tool to have in your arsenal and it makes performance and load testing your site extremely fun.

I recorded a quick screencast that shows me walking through my testing of the transient lock and I thought I'd share it here.

Enjoy!

{% include responsive-embed url="https://www.youtube.com/watch?v=yKxwlqZMVeo" %}