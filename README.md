---
title : Introduction to git using GitHub Desktop
part of : BITSS Summer 2016
time : 90 minutes
---

# Introduction

## Motivation

Essentially, we are trying to avoid a situation like this one :

![Version History](http://www.phdcomics.com/comics/archive/phd101212s.gif)

At a fundamental level, the problem is that we do not create perfect products the first time around. We add to them, remove things from them, and revise them heavily. For word processing tasks, like the PhD Comics example, this is somewhat harmless, and really is only costing you time in finding the correct document, or some embarrassment if you send the wrong document to a colleague.

If you are smart, you are already collecting, cleaning, reshaping, and analyzing your data in a way that is self documenting. That is to say, you are writing it in code, and are not modifying pieces of it by hand or in a GUI. The upside to this is reproducibility. The downside is that if any of your code is the wrong version, your whole pipeline gets bunked.

Unlike the situation above, when you can't find the right version of your processing pipeline, analytical workflow, or data, you also lose the ability to recreate any results that you've generated. If your results are not reproducible, then they are also :

1. Not verifiable
2. Not explainable
3. not extendable

So, we need a way to know which version of our pipeline we are using and what has changed since the last version.

## Background

There are many potential solutions in this space. Some people organize their revisions by hand into series of separate folders. Others use software that logs every action they take (SPSS or STATA output logs). Yet others prefer some kind of track-changes function in their GUI.

These solutions all suffer the same problem in that they force you, the user, to think about what a version is and how you are managing changes between versions. For example, if you are documenting your workflow with SPSS logs, if you want to know how you got that result you found one time last week, you have to manually search through the output from that entire day to find the code you ran but also all of the code that you ran to may or may not have led up to that result.

`git` is software that abstracts away those details; however, `git` is not particularly intuitive or user friendly. In fact, the author of `git` likes to joke that its name is a reference to how obstinate and curmudgeonly it is. The downsides here are:

1. Hard to understand
2. Hard to use correctly

However, the upsides are:

1. Never not once ever accidentally deleting or otherwise losing a file
2. Always being able to revert to your last working pipeline
3. Easy to discover what has changed (i.e. gone wrong), and when

Luckily for us, GitHub has built a GUI that makes working with `git` easier, although at some power cost.

# Getting started with `git`

## Registering for a GitHub account

* Go to [https://github.com/join](https://github.com/join)
* Follow instructions!
* A free/student account is fine
* You'll want to use the same email address that you used for git locally
* Choose a strong password!

![But not this one](http://imgs.xkcd.com/comics/password_strength.png)

## Enhancing your GitHub account

GitHub offers account upgrades for current students, that you can apply for at [https://education.github.com/](https://education.github.com/)

The education upgrade comes with:
* Free upgrade to a Micro account on GitHub (for writing code)
* Free Travis CI account (for testing code)
* Free SendGrid account (automated email API)
* 15USD in Amazon Web Services credits (for deploying code)
* 50USD in Digital Ocean credits (for deploying code)
* No transaction fees for your first 1000USD in sales via Stripe

## Forking repositories

We're going to use our new GitHub account to `fork`<sup>1</sup> a repository -- a repository for this class, as it just so happens!

* Navigate to [github.com/deniederhut/BITSS2016](github.com/deniederhut/BITSS2016)
* Look for a button that says "fork" in the upper right-hand corner
* Click it!

This repository will then be copied to your own account, so that you can make changes to it if you like. Since the fork exists on GitHub's servers, any changes that you push to those servers means those changes are already backed up for you!

## Installing GitHub Desktop

* Go to [https://desktop.github.com/](https://desktop.github.com/)
* Follow instructions!
* Open the app

Once you have opened GitHub Desktop, it will ask you to sign in with your GitHub account credentials (I hope you remembered your password!). Then, we are going to go to the left-hand side of the app, click the "+" button, and select "clone".

This is going to give you a list of all the repositories you have on GitHub (or any other upstream that you have added credentials for). Since you forked this repo earlier, you should see "BITSS2016" in that list. Go ahead and click it, and then click the clone button.

## A brief introduction to how GitHub Desktop works

In GitHub Desktop, a file can exist in one of two states:

1. Unmodified / committed
2. Modified

*Unmodified* files are files that `git` is keeping track of, but haven't been changed since the last time they were `committed`. We'll talk about what this means in a minute.

*Modified* files are files whose changes `git` is considering making permanent. To make a change permanent, `git` needs to know what changed (the file), who changed it (you), and when (`git` pulls the `date` from your system automatically). Making changes permanent is called `commit`ing them. Once a file has been committed to `git`, that version of it exists somewhere, forever, and the local file is considered an *unmodified* version of it.

# A standard workflow

1. First, we `pull` down any upstream changes to make sure we have the most up-to-date versions.
2. Next, we make a `branch` to contain the changes we want to make.
3. Then, we make whatever changes we want.
4. After that, we `commit` those changes
5. Then, we `merge` those changes into our
5. And finally, we `push` those changes

## Pulling

This one is pretty easy in GitHub Desktop. Select "Repository" from the menu at the top, and then choose "Pull". There should also be a keyboard shortcut.

Since you've just `clone`d this repository, there won't be any changes to pull in.

## Branching

If you're trying out something new, or making changes that you might not want to exist later, it's usually better to make a `branch` of your repository to work with. A branch is a copy of the entire repository that can be changed and discarded, or changed and merged back into the main branch.

It's a good idea to make separate branches to work on different parts of your workflow -- for example, one branch for you to try out changes to your data ingestion pipeline, and another for changes to your data analysis pipeline.

## Committing

Once you've changed some files in your repository, you can make those changes permanent by `commit`ting them. This allows you to revert back to that file, in that state, whenever you like, at any time in the future.

To commit files in GitHub Desktop, switch to the "Uncommitted changes" tab (you'll see it at the top of the app window). Any changed files will be listed on the left-hand side. By default, all changed files are selected, which is usually a bad thing. So, we start by unchecking the box to the left of "#n Changes".

Then, we choose which changes we want to commit, and click the check box next to those one by one.

Next, we need to add a summary of what has changed. This will be useful to us later when looking through the history, so make sure it is informative but short.

Finally, click the "Commit to branch" button at the bottom of that pane.

## Merging

Once you've made your changes in a branch, you can test them to make sure they do what you want them to do. Then, you'll want to bring those changes into your main branch by `merge`ing them.

First, we switch back into our `master` branch, from the branch button at the top of the screen.

Just underneath that button, in the history viewer, there is a button that says "compare". We'll click that one, and then select the branch we've been working on. This button should now say "Update from branch".

To merge in your changes, click that button!

## Pushing

This one is pretty easy in GitHub Desktop. Select "Repository" from the menu at the top, and then choose "Push". There should also be a keyboard shortcut.

Hooray! Your changes are committed locally, and backed up externally.

# Common tasks

## I want to undo local changes to a file

1. Go to the changes tab
2. Right-click the file
3. Select "Discard changes..."

## I want to undo my last commit

1. Select "Repository" from the menu at the top
2. Select "Undo most recent commit"

## I want to undo any commit

1. Go to the history tab
2. Select the commit you want to undo
3. Click the cog wheel
4. Select "Revert this commit"

## I want to change the commit message

1. Undo the last commit
2. Recommit the changes with a different message

---

For further information, you can check out<sup>2</sup>:
* [D-Lab's git fun!damentals materials](https://github.com/dlab-berkeley/git-fundamentals)
* [GitHub's introduction to git](https://try.github.io/)
* [A visual guide to git](https://marklodato.github.io/visual-git-guide/index-en.html)
* [The great book of git](https://git-scm.com/book/en/v2).

**1.** For more on forking, see [https://help.github.com/articles/fork-a-repo/](https://help.github.com/articles/fork-a-repo/)
**2.** Not `checkout`
