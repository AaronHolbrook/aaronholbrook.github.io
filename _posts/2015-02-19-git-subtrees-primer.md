---
title: "Git Subtrees - A Primer"
permalink: "git-subtrees-primer"
excerpt: "What are subtrees, why are they useful and how can they be used?"
categories:
  - Screencast
  - Git
---

<h2>Problem</h2>

Difficult to modularize code and maintain separate repos. Submodules are difficult or problematic to use.

<h2>Solution</h2>
Git Subtrees allow you to track and update a repo within a repo without the headache of submodules.

For a more in depth read on what / why - check out Vinicius' awesome <a href="https://medium.com/medium-eng/how-we-modularized-mediums-ios-codebase-8f8f26965c76">article</a>.

{% include responsive-embed url="http://www.youtube.com/embed/E7YWeRFHpXg" %}

<h2>Setup</h2>
Add remote to repo:

```bash
git remote add my-subtree git@github.com:account/project.git
```

Add subtree

```bash
git subtree add --prefix=path/to-repo repo-name branch
```

Push back to subtree's repo:

```bash
git subtree push --prefix=path/to-repo repo-name branch
```

Pulling changes from subtree's repo back to main repo:

```bash
git subtree pull --prefix=path/to-repo repo-name branch
```

Reference: [https://medium.com/@v/git-subtrees-a-tutorial-6ff568381844](https://medium.com/@v/git-subtrees-a-tutorial-6ff568381844)