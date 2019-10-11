---
layout: post
title:      "How to sync your fork with the parent repository"
date:       2019-10-11 19:45:44 +0000
permalink:  how_to_sync_your_fork_with_the_parent_repository
---


When working with git and GitHub, it's important to make sure that your forked and cloned repo is even with the parent repository, otherwise changes you make will be updating a previous version of the repository, and this could lead to some understandable problems. Here's how to sync your fork with the parent repository.

Right now, my fork of dev.to displays this message:

![This branch is 9 commits behind thepracticaldev:master](https://thepracticaldev.s3.amazonaws.com/i/208her37i9ft8ycylcpc.png)

How do I update my fork so that it's the same as thepracticaldev:master?

`cd` into the directory of your cloned repo

![cd code/open_source/dev.to](https://thepracticaldev.s3.amazonaws.com/i/tio9qd2e4clbjp08yezp.png)

Running `git remote -v` will display your current remotes

![git remote -v displays my fork as the only remotes](https://thepracticaldev.s3.amazonaws.com/i/c3up9vni4wz5shf8u3sf.png)

Add the parent repository as a new remote, specifying it as the upstream repository. In this example, we will run 

```
git remote add upstream https://github.com/thepracticaldev/dev.to.git
```

Verify with `git remote -v`

![git remote -v shows thepracticaldev/dev.to as the upstream repository](https://thepracticaldev.s3.amazonaws.com/i/a0610ow7r1htqrosbqw7.png)

`git fetch` the upstream repository

![Alt Text](https://thepracticaldev.s3.amazonaws.com/i/sm7lt8mdb3q9iniady8q.png)

The commits that are different from my fork are now in separate branches in my local environment. Let's merge those.

![Alt Text](https://thepracticaldev.s3.amazonaws.com/i/6bwcigatxwn1pf8ur0pz.png)

Now my cloned repo looks just like the upstream repository.

NOTE: any changes made locally before the merge are preserved, so you don't have to worry about losing any of your work when you do this.

From now on, whenever I need to sync with the upstream repository, all I need to do is fetch and merge.

At this point, running `git push` will update the forked repo and display this message:

![This branch is even with thepracticaldev:master](https://thepracticaldev.s3.amazonaws.com/i/c6b858pn4d64prcw8oi1.png)
