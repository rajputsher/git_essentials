# Rebasing

## Rebase commits

- Take commits from a branch and replay them at the end of another branch 
- Useful to integrate recent commits without merging
- maintains a cleaner, more linear project history 
- Ensures topic branch commits apply cleanly

Example: 
1. We have created a new_feature branch and have made 2 commits.<br/>
<img src="images/1.png" width=400 height=100>

2. By rebasing we are moving the new_feature branch and putting them at the beginning of the master branch.<br/>
<img src="images/2.png" width=400 height=100>

3. With that the SHA of those commits will change. <br/>
<img src="images/3.png" width=400 height=100>



A slightly more detailed version of what's actually happening.
-  When we say that we want to rebase the commits a new feature off of master, what git does is it starts rewinding the new feature branch, or picking up each one of those commits and putting them into temporary storage, and it keeps doing that until it gets back to a commit where it diverged from the master branch. <br/>
<img src="images/4.png" width=400 height=150>
<img src="images/5.png" width=400 height=150>

- Then, it moves to the tip of the master branch, and it replays each one of those commits. So, while it may be conceptually useful to think of just shifting your branch down to the end, what it's actually doing is picking up each one of those commits, one-by-one, and then replaying them at the end. <br/>
<img src="images/6.png" width=400 height=150>
<img src="images/7.png" width=400 height=100>

- That's useful because, as we'll see later, we don't have to just move it to the tip of master. We can pick up the commits that are in new feature, and we can move them to the tip of our master branch, to the tip of our redesign branch, or to the tip of an e-commerce branch. It's up to us. In every case, git is just going to pick up the commits, and then replay them where we tell it. <br/>
<img src="images/8.png" width=400 height=200>


How to rebase? 
- To rebase current branch to the tip of the master <br/>
`git rebase master`.
- To rebase a specific branch to tip of the master <br/> `git rebase master new_feature`

Useful for visualizing branches: <br/>
`git log --graph --all --decorate --oneline`

Return commit where topic branch diverges: <br/>`git merge-base master new_feature`
