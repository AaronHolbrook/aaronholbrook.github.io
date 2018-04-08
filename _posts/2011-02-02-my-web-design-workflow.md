---
title: "My Web Design Workflow"
---
<a href="http://www.reddit.com/user/hifiDesign">hifiDesign</a> over on <a href="http://www.reddit.com/r/Wordpress/comments/fcoqm/request_wordpress_svn_workflow/">Reddit</a> asked the question of how to use WordPress and SVN (or git in this case). Here is my more extended answer:

I develop primarily on two mac computers, synced via DropBox.

For local development I use MAMP.

I start by locally installing the latest version of WordPress to a clean directory in DropBox. I usually set up a new DB in PhpMyAdmin and get rolling with the new install.

Once the install is up and running it's time to work on the theme.

I initialize a git repository.

```bash
git init
```

And commit

```bash
git add . 
git commit -m "Initial Commit"
```

Oh - a sidenote here, I find TextExpander is an awesome helper here. I set up a couple abbreviations to help with the git commands that I use all the time. For example `gita` = `git add .` and `gitc` = `git commit -am "%|"`.

Once the git repo has been establish it's time to start developing.

Once I'm happy with development and need to have a live version for testing or for review I set up my live hub and live prime repos. Many thanks to Joe Maller for writing a [kickass tutorial](http://joemaller.com/990/a-web-focused-git-workflow/) on this.

SSH capabilities to your server are a must. If you don't have them - ask your provider. If they still don't budge, perhaps it's time to move to a better host.

After I've gotten the bare repo set up in a non-http accessible portion of my server than I install WordPress on the server, get it configured and initialize the 'prime' version git repo in the theme folder.

Locally I set up a hub remote to the bare hub repo we created

```bash
git remote add hub ssh://111.111.11.111:/home/bare_git_repo.git/
```

And force push master to the hub

```bash
git push -f hub master
```

Add hub as a remote for prime and force pull to get in sync

```bash
git remote add hub /home/bare_git_repo.git
git pull -f hub master
```

And there you have it. Don't forget if you're following along to review Joe Maller's guide and make sure you set up your post-commit and post-update hooks which allow you to automatically update the prime repo when you push to hub.

Also a word of caution: be aware if you edit files on the server live, you have to SSH in and sync back your other repos or it'll get out of sync and you'll have to reset. I've been using this setup for a couple months and haven't once felt the need to fire up a FTP program, live-edit a file and save it and see if it works. Instead I've found editing the same file locally, testing locally and then doing a quick

```bash
git add .
git commit -am "commit"
```

is much quicker and easier. Your mileage may vary however.