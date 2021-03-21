## Reset Types

- Reset changes the files in the staging index and/or working directory to the state they had when a specified commit was made.

- "Make my project look like it did back then"

- Moves HEAD pointer to a specific commit
- Types of reset : soft, mixed, hard.

### soft reset 

- Moves HEAD pointer
- Does not change the staging index
- Does not change the working directory
- usage: `git reset --soft <tree-ish>`

A soft reset is the simplest, it moves the head pointer to the specified commit but it does not change the staging index, it does not change the working directory. So essentially we're just moving the recording head where our next commit will go to another place in our commit tree.

When to use soft reset: 
- To return to an old state and leave code changes staged
- Useful for amending one or more commits
- Similar to `git commit --amend`
- Previous commits will be discarded 
- Becareful about amending commits which have been shared.

Creating a new branch and to checkout to that branch and branch with a particular starting point. In the below example we will create a new branch called reset_branch and with shorten_the_text commit.

```
>> git checkout -b reset_branch shorten_the_text
Switched to a new branch 'reset_branch'
>> git status
On branch reset_branch
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   4_explore_california/contact.html
        modified:   4_explore_california/explorers.html
        modified:   4_explore_california/index.html

>> git commit -am "commit A"
[reset_branch 8acc1e0] commit A
 3 files changed, 3 insertions(+), 3 deletions(-)

>> git status
On branch reset_branch
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   4_explore_california/mission.html
        modified:   4_explore_california/resources.html
        modified:   4_explore_california/tours.html

>> git commit -am "commit B"
[reset_branch cd935de] commit B
 3 files changed, 3 insertions(+), 3 deletions(-)

>> git log --oneline
cd935de (HEAD -> reset_branch) commit B
8acc1e0 commit A
b4a71f8 (shorten_the_text) Readme updated with branch compare
61f31d9 Changed the text by adding 'repo' at the end
f796556 Shortened the text
36e6994 (test_git_branch) Add file to new_feature branch
aca2cde commit before creating new_feature branch
```

Now we realised, there was no need to do 2 seperate commits, instead we want to do all the changes in one commit.  Before perfomring the soft reset copy the SHA of the head cd935de

1. `git reset --soft HEAD^` : we are saying to reset and go to parent of the HEAD.
```
> git reset --soft HEAD^

>> git log --oneline
8acc1e0 (HEAD -> reset_branch) commit A
b4a71f8 (shorten_the_text) Readme updated with branch compare
61f31d9 Changed the text by adding 'repo' at the end
f796556 Shortened the text
36e6994 (test_git_branch) Add file to new_feature branch

>> git status
On branch reset_branch
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   4_explore_california/mission.html
        modified:   4_explore_california/resources.html
        modified:   4_explore_california/tours.html
```
Here we can see the commit B is gone. and the status now shows all the changes that needs to be commited and are in the staging index.

2. If we now still need to have commit B we can go back using the command `git reset --soft cd935de`
3. If we make any commit from after point 1, the commit B will be gone and no more available.
4. Lets us say we moved back to commit B and now we want to make both the changes from commit A and commit B in one commit, we can do that as follows: 

```
>> git reset --soft HEAD^^

>> git status
On branch reset_branch
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   4_explore_california/contact.html
        modified:   4_explore_california/explorers.html
        modified:   4_explore_california/index.html
        modified:   4_explore_california/mission.html
        modified:   4_explore_california/resources.html
        modified:   4_explore_california/tours.html

>> git log -4 --oneline
b4a71f8 (HEAD -> reset_branch, shorten_the_text) Readme updated with branch compare
61f31d9 Changed the text by adding 'repo' at the end
f796556 Shortened the text
36e6994 (test_git_branch) Add file to new_feature branch
```
Now we can see in the log that both commit A and commit B are removed, we can make a new commit containing all the changes that are staged.

```
>> git commit -m "Commit AB"
[reset_branch ec7f08e] Commit AB
 6 files changed, 6 insertions(+), 6 deletions(-)

>> git log -4 --oneline
ec7f08e (HEAD -> reset_branch) Commit AB
b4a71f8 (shorten_the_text) Readme updated with branch compare
61f31d9 Changed the text by adding 'repo' at the end
f796556 Shortened the text
```



### Mixed Reset 

- Moves HEAD pointer
- Changes staging index to match repository
- Does not change the working directory
- usage: `git reset --mixed <tree-ish>` this is the default when we just use `git reset`.


```
>> git status
On branch reset_branch
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   4_explore_california/explorers.html
        modified:   4_explore_california/index.html

>> git commit -am "some edits"
[reset_branch ed30780] some edits
 2 files changed, 3 insertions(+), 3 deletions(-)

>> git commit -am "some edits"
[reset_branch ed30780] some edits
 2 files changed, 3 insertions(+), 3 deletions(-)
 
>> git log --oneline -3
ed30780 (HEAD -> reset_branch) some edits
ec7f08e Commit AB
b4a71f8 (shorten_the_text) Readme updated with branch compare
```

Let us start with copying the SHA of the HEAD, ed30780.
1. `git reset --mixed HEAD^` or just `git reset HEAD^`
```
>> git reset --mixed HEAD^
Unstaged changes after reset:
M       4_explore_california/explorers.html
M       4_explore_california/index.html

>> git status
On branch reset_branch
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   4_explore_california/explorers.html
        modified:   4_explore_california/index.html

>> git log --oneline -3
ec7f08e (HEAD -> reset_branch) Commit AB
b4a71f8 (shorten_the_text) Readme updated with branch compare
61f31d9 Changed the text by adding 'repo' at the end
```
Here we can see, the difference between mixed and soft reset is that  in mixed it rolls back to the working directory, and in the soft to the staged index.

2. Now that we have rolled back, now I want to commit changes to 2 files in 2 different commits.

```
>> git add .\4_explore_california\index.html

>> git commit -m "some edits to index file"
[reset_branch 8dd744c] some edits to index file
 1 file changed, 1 insertion(+), 1 deletion(-)

>> git commit -am "some edits to explorers file"
[reset_branch 4b17b69] some edits to explorers file
 1 file changed, 2 insertions(+), 2 deletions(-)

>> git log --oneline -3
4b17b69 (HEAD -> reset_branch) some edits to explorers file
8dd744c some edits to index file
ec7f08e Commit AB
```
Here we have removed "some edits" and made two sperate commits.

### Hard Reset 

- Moves HEAD pointer
- Changes staging index to match repository
- Changes the working directory to match repository
- usage: `git reset --hard <tree-ish>` 

Whe we use hard reset :
- It will return to an old state and discard all code changes
- It will permantly undo commits.
- Previous commits and all changes will be discarded

```
>> git log -3 --oneline
4b17b69 (HEAD -> reset_branch) some edits to explorers file
8dd744c some edits to index file
ec7f08e Commit AB
```

The Hard reset. 
1.  `git reset --hard HEAD^` 

```
>> git reset --hard HEAD^
HEAD is now at 8dd744c some edits to index file

>> git log -3 --oneline
8dd744c (HEAD -> reset_branch) some edits to index file
ec7f08e Commit AB
b4a71f8 (shorten_the_text) Readme updated with branch compare

>> git status
On branch reset_branch
```
Here we can see, by doing Hardreset it will completely rollback the previous commits.

When should we use Hard reset?

- If we want to make one branch look exactly same as another, we can do that with hard reset.

```
git log -3 --oneline
8dd744c (HEAD -> reset_branch) some edits to index file
ec7f08e Commit AB
b4a71f8 (shorten_the_text) Readme updated with branch compare

>> git branch
  master
* reset_branch
  shorten_the_text
  test_git_branch

>> git reset --hard shorten_the_text
HEAD is now at b4a71f8 Readme updated with branch compare

>> git status
On branch reset_branch

>> git log -3 --oneline
b4a71f8 (HEAD -> reset_branch, shorten_the_text) Readme updated with branch compare
61f31d9 Changed the text by adding 'repo' at the end
f796556 Shortened the text
```
We can see now the log shows the logs of the shorten_the_text branch.

