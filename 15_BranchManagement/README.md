# Branch Management

## Reason to Force push

Scenarios when we need force push: 

- Local version is better than the remote version
- Remote version went wrong and needs repair
- Versions have diverged and merging is undesirable

Usage : 
`git push -f` or `git push --force`

Consequences:

- Force push must be used carefully.
- Easy way to anger the whole development team
- Disruptive for others using the remote branch
- Commits disappear
- Subsequent commits are orphaned

Example: 

A collaborator has made changes to the file you were working on. 
```
>> git fetch
remote: Enumerating objects: 11, done.
remote: Counting objects: 100% (11/11), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 8 (delta 4), reused 7 (delta 3), pack-reused 0
Unpacking objects: 100% (8/8), done.
From https://github.com/rajputsher/git_essentials
   d71f72b..af9247c  master     -> origin/master

>> git status
On branch master
Your branch is behind 'origin/master' by 2 commits, and can be fast-forwarded.
  (use "git pull" to update your local branch)
```
You fetch the repository and see that your local is 2 commits behind the remote. You see the changes and you are not happy about the changes.

```
>> git diff master..origin/master
diff --git a/15_BranchManagement/ToDoList.txt b/15_BranchManagement/ToDoList.txt
index 70e82de..1d555c8 100644
--- a/15_BranchManagement/ToDoList.txt
+++ b/15_BranchManagement/ToDoList.txt
@@ -8,3 +8,8 @@ Afternoon
 ==========
 Prepare presentation for customer demo
 Review the new architecture
+Develop feature Alien
+
+Evening
+===========
+Get grocery
\ No newline at end of file
```

Now you ignore this change , inform you collaborator that you are doing a force push .
```
>> git status
On branch master
Your branch and 'origin/master' have diverged,
and have 1 and 2 different commits each, respectively.
  (use "git pull" to merge the remote branch into yours)

>>  git log --oneline -3 master
182170b (HEAD -> master) Updated todo for evening
d71f72b To do list for Afternoon
5dffa96 To do list for Morning

>> git log --oneline -4 origin/master
af9247c (HEAD -> master, origin/master, origin/HEAD) Updated todo for Evening
f71f48c Add develop feature alien to the list
d71f72b To do list for Afternoon
5dffa96 To do list for Morning

>> git push --force
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 391 bytes | 130.00 KiB/s, done.
Total 4 (delta 2), reused 0 (delta 0)
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To https://github.com/rajputsher/git_essentials.git
 + af9247c...182170b master -> master (forced update)

>> git log --oneline -4 origin/master
182170b (HEAD -> master, origin/master) Updated todo for evening
d71f72b To do list for Afternoon
5dffa96 To do list for Morning
6818188 Collaboration workflow
```
Here we can see the log on the remote, it changed to the one on the master and this is now pushed to the remote.

Now on the collaborator side: 

1. He needs to fetch the changes `git fetch` this will indicate him that there is a forces update

```
>> git fetch
remote: Enumerating objects: 7, done.
remote: Counting objects: 100% (7/7), done.
remote: Compressing objects: 100% (1/1), done.
remote: Total 4 (delta 2), reused 4 (delta 2), pack-reused 0
Unpacking objects: 100% (4/4), done.
From https://github.com/rajputsher/git_essentials
 + af9247c...182170b master     -> origin/master  (forced update)
```

2. Still the collaborator has the 2 commits from before
```
>> git log --oneline -4
af9247c (HEAD -> master) Updated todo for Evening
f71f48c Add develop feature alien to the list
d71f72b To do list for Afternoon
5dffa96 To do list for Morning

>> git log --oneline -4 origin/master
182170b (origin/master, origin/HEAD) Updated todo for evening
d71f72b To do list for Afternoon
5dffa96 To do list for Morning
6818188 Collaboration workflow
```

3. For collaborator to be pointing at the same commit as remote he should use `git pull` or better `git reset --hard origin/master`

```
>> git reset --hard origin/master
HEAD is now at 182170b Updated todo for evening

>> git log --oneline -4
182170b (HEAD -> master, origin/master, origin/HEAD) Updated todo for evening
d71f72b To do list for Afternoon
5dffa96 To do list for Morning
6818188 Collaboration workflow
```

Now the log of the collaborator and that I commited are same.

> Therefore, doing a forced push is simple but the impact on the collaborators is big.


## Deleting local and remote branches

To delete a branch, we must be on a different branch than the one we want to delete.
`git branch -d new_feature`, here the new_feature branch will be deleted only if this branch is fully merged with the existing branches. IF we still want to delete the branch that is not completely merged in to any of the existing branches we use -D instead of -d : `git branch -D new_feature`.


### Deleting a remote branch

1. `git push origin :new_feture` or in general <br/> `git push origin <local>:<remote>`

2. The more intuitive method from git v1.7.0+ :<br/> `git push --delete origin new_feature`. 
3. From version v2.8.0+ :<br/> `git push -d origin new_feature`

## Prune stale branches 

Stale branch is a remote-tracking branch that no longer tracks anything because the actual branch in the remote repository has been deleted.

Remote branches :
1. Branch on the remote repository(bugfix)
2. Local snapshot of the remote branch (origin/bugfix)
3. Local branch, tracking the remote branch(bugfix)

`git remote prune origin` #Delete stale remote-tracking branches

`git remote prune origin --dry-run` # To see what will be deleted before deleting.

Example: 

```
>> git checkout -b prune_test
Switched to a new branch 'prune_test'
M       15_BranchManagement/README.md

>> git push -u origin prune_test
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 8 threads.
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 417 bytes | 139.00 KiB/s, done.
Total 4 (delta 2), reused 0 (delta 0)
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
remote:
remote: Create a pull request for 'prune_test' on GitHub by visiting:
remote:      https://github.com/rajputsher/git_essentials/pull/new/prune_test
remote:
To https://github.com/rajputsher/git_essentials.git
 * [new branch]      prune_test -> prune_test
Branch 'prune_test' set up to track remote branch 'prune_test' from 'origin'.

>> git branch
  master
  non_tracking
* prune_test
  reset_branch
  shorten_the_text
  test_git_branch
  text_edits

>> git branch -r
  origin/master
  origin/non_tracking
  origin/prune_test
  origin/reset_branch
  origin/shorten_the_text
  origin/test_git_branch
  origin/text_edits
```

Now if we delete the branch, using `git push --delete origin prune_test`, both the remote and the local branch will be delted, but if the collaborator deletes it, we need to perform the prune. 

Lets us see how the collaborator deletes the branch: 
```
>> git branch -r
  origin/HEAD -> origin/master
  origin/master
  origin/non_tracking
  origin/prune_test
  origin/reset_branch
  origin/shorten_the_text
  origin/test_git_branch
  origin/text_edits

>> git push origin :prune_test
To https://github.com/rajputsher/git_essentials.git
 - [deleted]         prune_test

>> git branch -r
  origin/HEAD -> origin/master
  origin/master
  origin/non_tracking
  origin/reset_branch
  origin/shorten_the_text
  origin/test_git_branch
  origin/text_edits

>> git branch
* master
  non_tracking
```
Here we can see that for the collaborator who deleted the branch, both the local and remote branches were deleted.

Back to our repository.
```
>> git branch -r
  origin/master
  origin/non_tracking
  origin/prune_test
  origin/reset_branch
  origin/shorten_the_text
  origin/test_git_branch
  origin/text_edits

>> git fetch

>> git branch -r
  origin/master
  origin/non_tracking
  origin/prune_test
  origin/reset_branch
  origin/shorten_the_text
  origin/test_git_branch
  origin/text_edits
```
Even after doing `git fetch` the remote branch was not deleted for us by git. 
We need to do it our-selves by pruning. It is always recommented to check what would be pruned using --dry-run option.

```
>> git remote prune origin --dry-run
Pruning origin
URL: https://github.com/rajputsher/git_essentials.git
 * [would prune] origin/prune_test

>> git remote prune origin
Pruning origin
URL: https://github.com/rajputsher/git_essentials.git
 * [pruned] origin/prune_test

>> git branch -r
  origin/master
  origin/non_tracking
  origin/reset_branch
  origin/shorten_the_text
  origin/test_git_branch
  origin/text_edits
```

If you want to get the pruned branches when you fetch. <br/> Use: 1. `git fetch --prune` or `git fetch -p`
2. Or change the global config to do so: `git config --global fetch.prune true`

Following are not same as `git remote prune` they are completely different: <br/>
`git prune`#Prune all the unreachable objects <br/>
`git gc` #Part of garbage collection

