## Difference between files

`git diff`

Ex: 
```
> git diff
diff --git a/3_Diff_Delete_Move_Rename/Firstfile.txt b/3_Diff_Delete_Move_Rename/Firstfile.txt
index 2798193..b386c98 100644
--- a/3_Diff_Delete_Move_Rename/Firstfile.txt
+++ b/3_Diff_Delete_Move_Rename/Firstfile.txt
@@ -1,3 +1,3 @@
 This is the First file added to this project folder.

-Added second text line to the third line of the file.
\ No newline at end of file
+Added second text line to the third line of this file.
\ No newline at end of file
diff --git a/3_Diff_Delete_Move_Rename/SecondFile.txt b/3_Diff_Delete_Move_Rename/SecondFile.txt
index 2457836..525314d 100644
--- a/3_Diff_Delete_Move_Rename/SecondFile.txt
+++ b/3_Diff_Delete_Move_Rename/SecondFile.txt
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

## Delete Files

