---
title: "Git Bisect"
permalink: "troubleshooting-git-bisect"
categories:
  - Git
  - Programming
---

One of the lowest hanging fruits to learn is how to fix code regressions quickly and easily with `git bisect`.

Let's say you have some website that has a bug in a feature that, previously, was working fine (and that this is not all new functionality). We can actually use our version control system to find the exact commit the bug was created.

Not only can we pinpoint the bug, but `git bisect` allows us to find it faster than if we were to attempt to check out every commit and see if the bug was present or not.

To begin, let's run

```bash
git bisect start
```

Now since, we already know the bug is present, let's tell `git bisect` that this commit is `bad`

```php
git bisect bad
```

Now here's the really slick part - all we need to do is find a commit where the bug is not present. For the sake of argument, let's say that was 4 months ago and there have been hundreds of commits in between. No sweat, because since we'll be halving the number of commits we are checking (literally, we are bisecting it each time) we can quickly hone in on which commit introduced the bug.

So let's find a good commit (check it out and test to see if the bug is still present). If it is not then we now have our starting point.

We can now tell `git bisect` that this commit is `good`.

```php
git bisect good
```

This will begin a process where git will automatically check out the commit that is halfway between the good and bad commits. Simple do a `git bisect good` or `git bisect bad` if the bug is present or not. This will take a few steps, but typically no more than a handful.

At the end of the process, git will politely tell you which commit introduced the bug. This gives you a really great point to figure out exactly what change has caused the problem.