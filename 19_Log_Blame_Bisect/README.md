## Git log

- Log is the primary interface to git 
- Log has many options such as Sorting, filtering, output formating
- `git help log`

List commits as patches(diffs)
- `git log -p`
- `git log --patch`

List edits to lines 100-150 in filename.txt<br/>
`git log -L 100,150:filename.txt`

Examples:
```
>>git log -4
commit 3ee254bbabed0e171c923a7c2ce3f8ce11fd54b6 (HEAD -> master, origin/master)
Author: rajputsher <shersingh72@gmail.com>
Date:   Mon Apr 5 21:18:06 2021 +0200

    Git rebase

commit 59c26f9c842369a14ecb3e4a14c8317e2f43cf58
Author: rajputsher <shersingh72@gmail.com>
Date:   Mon Apr 5 21:14:55 2021 +0200

    Git rebase

commit fe4b75808a5806e9414e5854c1685ec2855a0a55 (expenses)
Author: rajputsher <shersingh72@gmail.com>
Date:   Mon Apr 5 21:08:49 2021 +0200

    Pull rebase

commit dbad5290c85d8f1170266dac5e2cd8c1381622fb
Author: rajputsher <shersingh72@gmail.com>
Date:   Mon Apr 5 20:58:39 2021 +0200

    interactive rebasing

>git log -p -1
commit 3ee254bbabed0e171c923a7c2ce3f8ce11fd54b6 (HEAD -> master, origin/master)
Author: rajputsher <shersingh72@gmail.com>
Date:   Mon Apr 5 21:18:06 2021 +0200

    Git rebase

diff --git a/18_Rebasing/README.md b/18_Rebasing/README.md
index 34a4211..70df938 100644
--- a/18_Rebasing/README.md
+++ b/18_Rebasing/README.md
@@ -173,8 +173,8 @@ How to choose ?

 `git rebase --onto newbase upstream branch`<br/>
 `git rebase --onto <new_base> <Old_branch it branched out of> <branch_to_rebase>`
-Example: `git rebase --onto master ecommerce new_feature`
-<img src="images/8.png" width=400 height=200>
+Example: `git rebase --onto master ecommerce new_feature` <br/>
+<img src="images/8.png" width=400 height=200><br/>
 Take new_feature branch off of the ecommerce branch and put it to the tip of the master branch.

 Example:
```

## git blame

Another debugging tool in Git, called blame. 
- Blame allows you to browse an annotated version of the file. The reason you would do that is it allows you to determine who changed which lines in the file and why. In other words who wrote this code or who should I blame, that's where it gets its name. 
- It can be useful for probing the history behind a file's current contents. 
- It's useful for identifying which commit in particular introduced a bug. 

Usage: 
- To Annotate file with commited details:`git blame filename.txt`
- To ignore whitespace `git blame -w filename.txt`
- To annotate lines 100-150: `git blame -L 100,150 filename.txt`
- To annotate lines 100-150: `git blame -L 100,+50 filename.txt`
- All the above are for the current HEAD commit. If we want to annotate a file at revision abcd231<br/> `git blame abcd231 filename.txt`
- A lot of people feel that blame has a negative connotation to it, and so it's very common for Git developers to add an alias to their file called praise and in fact some source code management systems use praise as a synonym for blame so that either one works the same, so you can go with the positive version if you're trying to praise someone for their good work or the blame version if you're trying to figure out who did something wrong.Add a global alis for 'praise'<br/>`git config --global alias.praise blame`
- Similar to blame with slighlty different output format is annotate: `git annotate filename.txt`

Example:
```
>> git blame 15_BranchManagement\ToDoList.txt
5dffa962 (rajputsher 2021-03-29 20:07:46 +0200  1) Morning
5dffa962 (rajputsher 2021-03-29 20:07:46 +0200  2) ==========
5dffa962 (rajputsher 2021-03-29 20:07:46 +0200  3) Develop feature Alien
5dffa962 (rajputsher 2021-03-29 20:07:46 +0200  4) Call the housing company
d71f72bd (rajputsher 2021-03-29 20:09:13 +0200  5) Send the email to landlord
d71f72bd (rajputsher 2021-03-29 20:09:13 +0200  6)
d71f72bd (rajputsher 2021-03-29 20:09:13 +0200  7) Afternoon
d71f72bd (rajputsher 2021-03-29 20:09:13 +0200  8) ==========
d71f72bd (rajputsher 2021-03-29 20:09:13 +0200  9) Prepare presentation for customer demo
d71f72bd (rajputsher 2021-03-29 20:09:13 +0200 10) Review the new architecture
182170b2 (rajputsher 2021-03-29 20:34:57 +0200 11)
182170b2 (rajputsher 2021-03-29 20:34:57 +0200 12)
182170b2 (rajputsher 2021-03-29 20:34:57 +0200 13) Evening
182170b2 (rajputsher 2021-03-29 20:34:57 +0200 14) =========
182170b2 (rajputsher 2021-03-29 20:34:57 +0200 15) To to cinema
0c10d628 (rajputsher 2021-04-05 19:26:25 +0200 16) Eat at a restaurant
0c10d628 (rajputsher 2021-04-05 19:26:25 +0200 17)
0c10d628 (rajputsher 2021-04-05 19:26:25 +0200 18) Shopping
0c10d628 (rajputsher 2021-04-05 19:26:25 +0200 19) =========
0c10d628 (rajputsher 2021-04-05 19:26:25 +0200 20) milk
0c10d628 (rajputsher 2021-04-05 19:26:25 +0200 21) tomato
0c10d628 (rajputsher 2021-04-05 19:26:25 +0200 22) lemons
af728d9b (rajputsher 2021-04-05 20:08:28 +0200 23) lime
1a810c29 (rajputsher 2021-04-05 20:07:42 +0200 24) Apple
1a810c29 (rajputsher 2021-04-05 20:07:42 +0200 25) Orange

>> git blame -L 13,21 15_BranchManagement\ToDoList.txt
182170b2 (rajputsher 2021-03-29 20:34:57 +0200 13) Evening
182170b2 (rajputsher 2021-03-29 20:34:57 +0200 14) =========
182170b2 (rajputsher 2021-03-29 20:34:57 +0200 15) To to cinema
0c10d628 (rajputsher 2021-04-05 19:26:25 +0200 16) Eat at a restaurant
0c10d628 (rajputsher 2021-04-05 19:26:25 +0200 17)
0c10d628 (rajputsher 2021-04-05 19:26:25 +0200 18) Shopping
0c10d628 (rajputsher 2021-04-05 19:26:25 +0200 19) =========
0c10d628 (rajputsher 2021-04-05 19:26:25 +0200 20) milk
0c10d628 (rajputsher 2021-04-05 19:26:25 +0200 21) tomato

>> git annotate 15_BranchManagement\ToDoList.txt
5dffa962        (rajputsher     2021-03-29 20:07:46 +0200       1)Morning
5dffa962        (rajputsher     2021-03-29 20:07:46 +0200       2)==========
5dffa962        (rajputsher     2021-03-29 20:07:46 +0200       3)Develop feature Alien
5dffa962        (rajputsher     2021-03-29 20:07:46 +0200       4)Call the housing company
d71f72bd        (rajputsher     2021-03-29 20:09:13 +0200       5)Send the email to landlord
d71f72bd        (rajputsher     2021-03-29 20:09:13 +0200       6)
d71f72bd        (rajputsher     2021-03-29 20:09:13 +0200       7)Afternoon
d71f72bd        (rajputsher     2021-03-29 20:09:13 +0200       8)==========
d71f72bd        (rajputsher     2021-03-29 20:09:13 +0200       9)Prepare presentation for customer demo
d71f72bd        (rajputsher     2021-03-29 20:09:13 +0200       10)Review the new architecture
182170b2        (rajputsher     2021-03-29 20:34:57 +0200       11)
182170b2        (rajputsher     2021-03-29 20:34:57 +0200       12)
182170b2        (rajputsher     2021-03-29 20:34:57 +0200       13)Evening
182170b2        (rajputsher     2021-03-29 20:34:57 +0200       14)=========
182170b2        (rajputsher     2021-03-29 20:34:57 +0200       15)To to cinema
0c10d628        (rajputsher     2021-04-05 19:26:25 +0200       16)Eat at a restaurant
0c10d628        (rajputsher     2021-04-05 19:26:25 +0200       17)
0c10d628        (rajputsher     2021-04-05 19:26:25 +0200       18)Shopping
0c10d628        (rajputsher     2021-04-05 19:26:25 +0200       19)=========
0c10d628        (rajputsher     2021-04-05 19:26:25 +0200       20)milk
0c10d628        (rajputsher     2021-04-05 19:26:25 +0200       21)tomato
0c10d628        (rajputsher     2021-04-05 19:26:25 +0200       22)lemons
af728d9b        (rajputsher     2021-04-05 20:08:28 +0200       23)lime
1a810c29        (rajputsher     2021-04-05 20:07:42 +0200       24)Apple
1a810c29        (rajputsher     2021-04-05 20:07:42 +0200       25)Orange

>>git config --global alias.praise blame

>>git praise -L 13,21 15_BranchManagement\ToDoList.txt
182170b2 (rajputsher 2021-03-29 20:34:57 +0200 13) Evening
182170b2 (rajputsher 2021-03-29 20:34:57 +0200 14) =========
182170b2 (rajputsher 2021-03-29 20:34:57 +0200 15) To to cinema
0c10d628 (rajputsher 2021-04-05 19:26:25 +0200 16) Eat at a restaurant
0c10d628 (rajputsher 2021-04-05 19:26:25 +0200 17)
0c10d628 (rajputsher 2021-04-05 19:26:25 +0200 18) Shopping
0c10d628 (rajputsher 2021-04-05 19:26:25 +0200 19) =========
0c10d628 (rajputsher 2021-04-05 19:26:25 +0200 20) milk
0c10d628 (rajputsher 2021-04-05 19:26:25 +0200 21) tomato
```

## Git Bisect

- Bisect allows us to find the commit that introduced a problem to our code, either a bug or a regression. 
- We use bisect when we know that there's a problem in a particular version and we know that there didn't use to be that problem. We want Git to help us identify which commit between the good version and the bad version created the issue. so you'll tell bisect the last known good revision and you'll tell it the first known bad revision. And then bisect will automate a process to help you figure out where in between those did things go wrong. It does that by resetting the code to the midpoint. 
- So we've essentially checked out a version of the code that's in between the two and we're going to check there and see are things good or bad. And it's going to be your job to test. You'll poke around in the files. Maybe you want to view the project in a browser, or maybe you have a test suite of code that you want to run to see whether the tests pass or fail. Once we know whether the revision that's right at the midpoint is good or bad we'll mark it for bisect so that it knows.
- And then it will repeat the process using one of the halves of the search space. So if we've marked it as being a good revision, then this will now become the last known good revision. Or if we marked the midpoint as being a bad revision, this will be the first known bad revision. And it'll know to search either forwards or backwards based on that.

Usage:
- `git bisect start`
- `git bisect bad <treeish>` , `bad` or`new` `<treeish>` can be a branch name, a SHA , a tag or left blank then it would consider the HEAD.
- `git bisect good <treeish>`,  `good` or `old` can be used
- `git bisect reset `: will reset the working directory back to the head that you were at before you started bisecting.

Example:

1. 
```
>> git log --oneline 15_BranchManagement\ToDoList.txt
1a810c2 Update shopping list with orange
af728d9 Update shopping list with Apple
0c10d62 Todo: Shopping list updates
182170b Updated todo for evening
d71f72b To do list for Afternoon
5dffa96 To do list for Morning
```

2. Let us say we have a bug or in this case we never wanted to add Apple to the list, we can do the following:
    - `git bisect start`
    - `git bisect bad <SHA of the commit where bug is found>`
    - `git bisect good <SHA of the commit where there was no bug>`
    - Now git gives us a commit which in between the last known bad commit and good commit. We need to look in to the files at that commit and see if this is a bad or good commit, i.e if there is a bug or not.
    - if there is no bug in that we set that now as good `git bisect good <SHA of the good commit>`
    - We continue this until we find the commit where the bug was introduced.
    - Finally we do a reset to point back head to the latest commit on the branch `git bisect reset`

