---
title: "My solution to quickly syncing .bash_profile on multiple machines"
permalink: "/my-solution-to-quickly-syncing-bash_profile-on-multiple-machines/"
categories:
  - Programming
  - Linux
  - Server
---

You know that feeling when you're setting up a brand new server and it's not set up the way you've spent years tweaking it to be?

<figure class="align-center">
  <a href="#"><img src="{{ '/images/bash-profile-syncing-comfortable.png' | absolute_url }}" alt=""></a>
  <figcaption>Nice and comfy customized `.bash_profile`, even got my `ls` command to show hidden files by default!</figcaption>
</figure> 

As opposed to the following (setting up a new linux box, not even ls works how I like it).

<figure class="align-center">
  <a href="#"><img src="{{ '/images/bash-profile-syncing-yuck.png' | absolute_url }}" alt=""></a>
  <figcaption>Default. Ugh - beat it with the `.bash_profile` stick please!</figcaption>
</figure> 

After taking a brief glance at <a href="http://alias.sh">alias.sh</a>, I decided I wanted to be able to customize things just a little bit more to my liking.

I came up with the following workflow:
<ol>
	<li>Use GitHub to host a always-up-to-date published `.bash_profile`</li>
	<li>Use a TextExpander snippet to easily wget the `.bash_profile` from GitHub onto the new server</li>
	<li>[OPTIONAL] Keep my local work machine's aliases separate from remote production machines by separating them out into a `.bash_aliases` file</li>
	<li>[OPTIONAL] One more TextExpander snippet for the `.bash_aliases` to make things easy</li>
</ol>

<h2>Step 1</h2>

I published out my files in a new repo on GitHub, titled tersely enough: <a title="Aaron Holbrook's dotfiles" href="https://github.com/aaronholbrook/dotfiles">dotfiles</a>.

I went back and forth between GitHub and BitBucket, and even tried out BitBucket since they offer free private repositories, but unfortunately BitBucket's URLs for the RAW files include the commit hash, which would be changing with each commit, rendering my TextExpander snippet useless.

So - because I need the RAW file URL to be unchanging, I went with GitHub, even though it means publicizing all my current aliases. Oh well - enjoy :)

So - this gets us a public published RAW url that will not change:

[`https://raw.github.com/AaronHolbrook/dotfiles/master/.bash_profile`](https://raw.github.com/AaronHolbrook/dotfiles/master/.bash_profile)

<h2>Step 2</h2>
I use the following command:

```sh
wget -q -O - "$@" https://raw.github.com/AaronHolbrook/dotfiles/master/.bash_profile > ~/.bash_profile
```

and place it inside a TextExpander snippet with the shortcut of: `dotfilespullprofile`.

<h2>Step 3</h2>

For my personal use case, I prefer to have my command prompt styled and things like ls and stuff always the same, regardless of if I'm on my own machine or if I'm SSHed into a server. But there are certain aliases that shortcut me to some folders, however I don't really want those aliases to be on the server (as it'd be pointless and confusing).

Thus, I separated my aliases into a separate file, which .bash_profile only pulls in if it exists:

```bash
if [ -f ~/.bash_aliases ]; then
  . ~/.bash_aliases
fi
```

<h2>Step 4</h2>

I use the following command to pull in the `.bash_alias`.

```bash
wget -q -O - "$@" https://raw.github.com/AaronHolbrook/dotfiles/master/.bash_alias > ~/.bash_alias
```

<h2>Tada!</h2>
And there you have it, a quick and dirty way to sync your always-up-to-date `.bash_profile` onto new machines!