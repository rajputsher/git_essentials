# Stash Changes

## Stash changes in the stash

Without having to commit the changes, it's a lot like putting something into a drawer to save it for later. The Stash is not part of the repository, the staging index, or the working directory. It's a special fourth area of GIT, separate from the others.

When would we stash changes? Let us consider we are in the branch `shorten_the_text`, we make a minor change to the title of the mission.html file. and we want to now checkout to master branch. We get an error as below!!

```
> git checkout shorten_the_text
Switched to branch 'shorten_the_text'

>> git status
On branch shorten_the_text
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   4_explore_california/mission.html

>> git checkout master
error: Your local changes to the following files would be overwritten by checkout:
        4_explore_california/mission.html
Please commit your changes or stash them before you switch branches.
Aborting
```
As seen above git asks to commit the changes or stash them. Stash is saving the changes with a description as shown below. 

```
>> git stash save "Changed mission page title"
Saved working directory and index state On shorten_the_text: Changed mission page title

>> git status
On branch shorten_the_text
nothing to commit, working tree clean

>> git checkout master
Switched to branch 'master' 
```
Git by default will not stash the untracked files. To stash the untracked files we need to add options such as : `-u`, `--include-untracked` 

## View stashe changes

`git stash list`, to see the changes we can use `git stash show stash@{0}`. To see specific changes use: `git stash show -p stash@{0}` 

For windows: `git stash show "stash@{0}"` and `git stash show -p "stash@{0}"` 

```
>> git stash list
stash@{0}: On shorten_the_text: Changed mission page title

>> git stash show "stash@{0}"
 4_explore_california/mission.html | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)

>> git stash show -p "stash@{0}"
diff --git a/4_explore_california/mission.html b/4_explore_california/mission.html
index c0deb71..811e8b5 100644
--- a/4_explore_california/mission.html
+++ b/4_explore_california/mission.html
@@ -2,7 +2,7 @@
 <html lang="en">
   <head>
     <meta charset="utf-8">
-    <title>Explore California: Mission</title>
+    <title>Explore California: Our Mission</title>
     <link href="assets/stylesheets/main.css" rel="stylesheet" type="text/css" media="all">
     <script src="assets/javascripts/jquery-3.4.0.min.js"></script>
     <script src="assets/javascripts/menus.js"></script>
```

**Changes in the stash are independent of the branch you are on.** That means, we can be on the master branch change to another branch and we can use this changes in another branch.

## Retrieve stashed changes 

The changes made to the mission.html file cannot be seen in the file, because it is stash. To retrieve the stash, `git stash pop`, it will pop changes of the top of the stash list. If we want a particular stash we can specify as `git stash pop "stash@{n}"`.

```
>> git stash pop
On branch shorten_the_text
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   4_explore_california/mission.html

no changes added to commit (use "git add" and/or "git commit -a")
Dropped refs/stash@{0} (0b15e2c72c28bb3505d5e17d55a27396fd8948cd)
```
Now we can see the changes in the mission.html file, and now it is not commited yet. But we can see `git stash list` and it will return nothing, as all the stashes were retrieved.

If you want to retrieve the change but want to leave it in the stash, we can do that using `git stash apply` instead of `pop`. 

## Delete stashed changes

Adding another item to the stash list.

```
>> git stash list
stash@{0}: On shorten_the_text: Changed mission page title.

>> git status
On branch shorten_the_text
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   4_explore_california/mission.html
no changes added to commit (use "git add" and/or "git commit -a")

>> git stash save "Delete me"
Saved working directory and index state On shorten_the_text: Delete me

>> git stash list
stash@{0}: On shorten_the_text: Delete me
stash@{1}: On shorten_the_text: Changed mission page title.
```

There are few ways to delete items from the stash:

1. using `git stash pop`. This will remove the item and applies the changes to the working directory.
2.  using `git stash drop stash@{0}`

```
>> git stash list
stash@{0}: On shorten_the_text: Delete me
stash@{1}: On shorten_the_text: Changed mission page title.

>> git stash drop "stash@{0}"
Dropped stash@{0} (337ce02628451a97e64c3fd2a9a1d82e318e6d74)

>> git stash list
stash@{0}: On shorten_the_text: Changed mission page title.
```
3. `git stash clear`: clears all the stashed changes in the list.
