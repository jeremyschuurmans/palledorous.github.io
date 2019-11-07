---
layout: post
title:      "6 Git commands every beginner should memorize"
date:       2019-11-07 22:52:04 +0000
permalink:  6_git_commands_every_beginner_should_memorize
---


For people new to Git, it can be confusing and intimidating. If that's you, here are six Git commands for your toolbox. With these, you can become productive with Git and lay a solid foundation for your future Git mastery. Code along with these in order and learn them all!

Just a quick side note: this post is intended to be a quick, accessible breakdown of the most common Git commands I use every day, which were also the ones I had to look up most often when I was learning Git. My hope is that it will reduce the time it takes for someone new to Git to become productive with it.

It will be most useful to you if you already have a basic understanding of what Git is, a concept of how the Git workflow works (branching, merging, etc.), some command line knowledge, and have Git installed and configured on your system.

I use Ruby in all my examples.

### 1. git init

`git init` is how you add git to your project.

- open your terminal, and create a new directory. I keep all my code-related files in a `code` folder, so I'll put it there. You can put it wherever you like. `mkdir code/practice`

![mkdir code/practice](https://thepracticaldev.s3.amazonaws.com/i/ramaom7a0gzocpqpe3te.png)
 
- change to your newly created directory. `cd code/practice`

![cd code/practice](https://thepracticaldev.s3.amazonaws.com/i/d1fjxjsbe0nz84158ql6.png)

- create a new project directory named 'git-practice'. `mkdir git-practice`

- `cd` into it. `cd git-practice`

- run `git init`

![mkdir git-practice, then cd git-practice, then git init](https://thepracticaldev.s3.amazonaws.com/i/fhtrhd3l4a7cz5liz8xd.png)

this will create an empty Git repository, a `.git` directory inside your project directory.

### 2. git status

`git status` lets you see the current state of your files.

- create a file called "git_practice.rb". `touch git_practice.rb`

- run `git status`. Git will tell you that you are on the master branch, you have not made any commits, and it will list all untracked files you have, in this case, we only have one, `git_practice.rb`.

![touch git_practice.rb, then git status](https://thepracticaldev.s3.amazonaws.com/i/nijqsx2z47bdy4w9acim.png)

### 3. git add

`git add` is how you start tracking individual files.

- run `git add .` adding the <kbd>space</kbd> + <kbd>.</kbd> tells Git to add all files. You can also add individual files by running `git add <filename>`. This can be useful if you're ever in a situation where you want to add certain files in one commit, and other files in a different commit.

![git add .](https://thepracticaldev.s3.amazonaws.com/i/jtel1njj58etaql0dsbq.png)

If you run `git status` now, it'll show you changes ready to be committed, in this case, that we created a new file.

### 4. git commit

`git commit` creates a new commit.

- run `git commit -m` (the -m stands for message), and write "first commit" in quotation marks. `git commit -m "first commit"`

![git commit -m 'first commit'](https://thepracticaldev.s3.amazonaws.com/i/ip1ejym1wjf2k57vp347.png)

### 5. git checkout

You use `git checkout` to switch between branches. For convenience, you can abbreviate it to `git co ` If you add the `-b` flag, it will both create a new branch and switch to it at the same time. You can name your branches whatever you like, but descriptive names are best, like so: `git co -b add-example-code`

- running that command will create and switch to a branch called `add-example-code`.

![git co -b add-example-code](https://thepracticaldev.s3.amazonaws.com/i/c7crg50ncu1ncm9u874u.png)

- open `git_practice.rb` in your text editor of choice.

- add some code. Let's go with `puts 'Hello World!` Save the file.

- let's run `git status` again to see what happened. Again, it'll show you what branch you're on, and what changes you made that aren't staged for committing yet. In this case, that we modified git_practice.rb.

![git status](https://thepracticaldev.s3.amazonaws.com/i/5651n0rtidjjw8irmf3m.jpg)

- add and commit this file. `git add .` then `git commit -m "add hello world"`

![git add ., then git commit -m 'add hello world'](https://thepracticaldev.s3.amazonaws.com/i/g6a1ei8gfoza6lbllqyl.png)

### 6. git merge

You use `git merge` to integrate your branch with the master branch.

- switch to master. `git co master`

- run `git merge add-example-code`. This will integrate our add-example-code branch with master, so now all changes made in the branch are present in master.

![git co master, then git merge add-example-code](https://thepracticaldev.s3.amazonaws.com/i/z7tyqnpiuvjrozlir6ln.png)

With these commands you will be well on your way to productivity with git.

We're barely scratching the surface, however. Many good, in-depth resources for learning Git can be found [here](https://try.github.io/).
