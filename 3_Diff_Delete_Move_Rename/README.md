## Difference between files

`git diff`

Ex: 
```
> git diff
diff --git a/Firstfile.txt b/Firstfile.txt
index 2798193..b386c98 100644
--- a/Firstfile.txt
+++ b/Firstfile.txt
@@ -1,3 +1,3 @@
 This is the First file added to this project folder.

-Added second text line to the third line of the file.
\ No newline at end of file
+Added second text line to the third line of this file.
\ No newline at end of file
diff --git a/SecondFile.txt b/SecondFile.txt
index 2457836..525314d 100644
--- a/SecondFile.txt
+++ b/SecondFile.txt
@@ -1 +1,2 @@
-This is the Second file added to this folder.
\ No newline at end of file
+This is the Second file added to this folder.
+Second line of second file.
\ No newline at end of file
```


Other variations: 

1. `git diff --staged` : Difference between repository and staged commit
2. `git diff --cached`
3. `git diff --color-words` : Shows red and green only for the different contents.

What is the difference between `git diff` and `git diff --staged`?

`git diff` compares the changes to working directory files to the staging index, while `git diff --staged` compares staged files to the repository versions.

## Show contents of a particular commit

- `git show <commit_id>` : will show what was changed in that commit.
- `git show <commit_id> --color-words`

ex: `git show dbf341s`

## Delete Files

`git rm file_to_delete.txt` 


```
git rm file_to_delete1.txt
rm 'file_to_delete1.txt'
```

## Move and rename files 

1. After renaming a file in the folder Firstfile.txt --> Primaryfile.txt.
This shows as one file being deleted and one untracked file.

```
git status
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        deleted:    Firstfile.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        Primaryfile.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

2. `git add Primaryfile.txt` && `git rm Firstfile.txt` &&  `git status`
Now the git status, shows that git regonizes the renaming of the file.

```
On branch master

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        renamed:    Firstfile.txt -> Primaryfile.txt
```

## Use move to rename the file

Ex:

1. `git mv SecondFile.txt SecondaryFile.txt` && `git status`

```
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        renamed:    Firstfile.txt -> Primaryfile.txt
        renamed:    SecondFile.txt -> SecondaryFile.txt
```
2. `git mv ThirdFile.txt firstFolder\ThirdFile.txt` && `git status`

```
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        renamed:    Firstfile.txt -> Primaryfile.txt
        renamed:    SecondFile.txt -> SecondaryFile.txt
        renamed:    ThirdFile.txt -> firstFolder/ThirdFile.txt
```

## Git compare 

compare the changes between 2 specific git commits.

`git diff <commit_id1>..<commit_id2>`

Ex: 
1. `git diff b2326e79..fd840328 --color-words`
2. `git diff b2326e79..HEAD --color-words`


## Multiline git commit 

`git commit -a` enter, will open up a text editor to add the comments , here we can add multiple line commit message.