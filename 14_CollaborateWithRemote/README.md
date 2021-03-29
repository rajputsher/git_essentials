# Collaborate with remote

## Push Changes

Let us make changes to tours.html 
```
> git status
On branch master
Your branch is up to date with 'origin/master'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   4_explore_california/tours.html

no changes added to commit (use "git add" and/or "git commit -a")

>> git add .\4_explore_california\tours.html

>> git commit -m "Changes URL format on tours page"
[master a092b0a] Changes URL format on tours page
 1 file changed, 8 insertions(+), 8 deletions(-)

>> git log --oneline -3
a092b0a (HEAD -> master) Changes URL format on tours page
cacbf7b (origin/master) remote tracking, untracking
9555d7d git remote tracking

>> git log --oneline -3 origin/master
cacbf7b (origin/master) remote tracking, untracking
9555d7d git remote tracking
711754f (origin/non_tracking) Working with remote
```

Above we can see the log of master and origin/master. We can see that origin/master is one commit behind. we can see the changes : `git diff origin/master..master --color-words`

Now we have the changes locally, we need to push this to the remote.
`git push origin master` or `git push` if already on master.

## Fetch changes 

`git fetch` : Gets all that is on the remote repo to local repo. It is important to note that the local master will not be pointing to the origin\master yet. 

## Merge in fetched changes

`git merge origin/master` : i.e we are merging the origin/master with master.

We always need to use these 2 commands : `git fetch` + `git merge` or use `git pull` which will do both together.


