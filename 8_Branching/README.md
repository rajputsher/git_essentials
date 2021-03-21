# Git Branching

Branches are one of the most powerful features in Git, in large part because of how easy they are to use. It's as if Git wants you to branch, and getting the most out of Git will mean using branches often and effectively. 
- In Git, branches are cheap. They're easy to create, they don't take a lot of processor power, they don't take up a lot of storage space, they're easy to delete, and they're easy to work with. That means branches make it easy to try new ideas. 
- Let's imagine that you have your master branch that you're working on, and suddenly you get an idea for something, but you're not sure if it's going to work out or not. Instead of making a lot of commits to your master branch and then trying to undo those if it doesn't work out, instead, you can create a new branch and try your ideas there. If those ideas don't work out, you just throw away the branch, and you haven't tainted your master timeline with those mistakes. If it does work out, then you can fold those changes back into the master branch through a process called merging.

Example of branching :

<img src="images/1.png" width=400 height=100>

HEAD moves around depending on the tip of the current branch we are on.

<img src="images/2.png" width=400 height=100>

<img src="images/3.png" width=400 height=100>

## Creating branches

The command `git branch` will show us the available branches in the git repository.

```
git branch
* master
```
Here we have only master branch. and * indicates the current branch.


To create a new branch: `git branch new_feature` 

```
git branch
```

