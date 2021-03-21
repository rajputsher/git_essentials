## Reference Commits

### Tree-ish

A directory containing files and other directories(which git calls "trees") or any identifier which references a tree.

A commit is considered tree-ish because it refers to a tree at the point when a commit has been applied.

In simple terms, a tree-ish is  a directory, a commit or a reference. Ex: SHA-1 hash, HEAD pointer reference, Branch reference, Tag reference, Ancestry, etc.

**SHA-1 HASH**
- Complete 40-character string
- Minimum: 4 Characters 
- Unambiguous: 8-10 characters
- git show ad148963e

**HEAD Pointer**
- .git/HEAD : Points to the current head
- ex: .git/refs/heads/master
- We can simply use: `git show HEAD `

### Ancestry

***Parents***

We can get the parent of a commit using ^.

- ad148963e^
- HEAD^ : Parent of the HEAD commit
- master^: commit before the last commit in the master branch
- Alternatively: HEAD~1 or HEAD~ will do tha same.
- Usage: `git show HEAD^`

***Grandparents***

use two ^^ signs.

- ad148963e^^
- HEAD^^
- master^^
- Alternatively: HEAD~2
- Usage: `git show HEAD^^`

Similary for great-grandparent another ^ and so on.

### Tree-listings

We know that a tree in Git is just a directory. If we want to see how we can list the contents of that directory from inside Git, we can use the command: `git ls-tree <tree-ish>`. 

Description of `git help ls-tree`

```
Lists the contents of a given tree object, like what "/bin/ls -a" does in the current working directory. Note that:

- the behaviour is slightly different from that of "/bin/ls" in that the <path> denotes just a list of patterns to match, e.g. so specifying directory name (without -r) will behave differently, and order of the arguments does not matter.

- the behaviour is similar to that of "/bin/ls" in that the <path> is taken as relative to the current working directory. E.g. when you are in a directory sub that has a directory dir, you can run git ls-tree -r HEAD dir to list the contents of the tree (that is sub/dir in HEAD). You don’t want to give a tree that is not at the root level (e.g. git ls-tree -r HEAD:sub dir) in this case, as that would result in asking for sub/sub/dir in the HEAD commit. However, the current working directory can be ignored by passing --full-tree option.
```

Ex:  
- `git ls-tree HEAD`: Shows all the folders under the repository and their associated SHA-1 value.
- `git ls-tree HEAD .\1_GitInit\`: shows the files under the folder and its associated SHA-1 value.

### Filter the commit log

- `git log -3` : show the latest three commit.
- `git log --since=2020-13-03`: shows commit log since 13th march.
- `git log --until=2020-13-03`: shows commit log until 13th march.
- `git log --until="3 days ago"`
- `git log --after=2.weeks --before=3.days`
- `git log --author=<part of the name>`
- `git log --grep="Initial"`
- `git log SHA_1..SHA_2`: log between 2  commits. Ex: `git log bcd1256f..HEAD`
- `git log <file-name>`: log of the commit for a given file.

### Format the commit log

- `git log -p` : shows all the commit logs along with the changes done.
- `git log --stat`: Shows the statistics( 3 files changed, 216 insertions(+), 1 deletion(-) ) of the change but not the actual changes. ex:
```
commit fd840328a58eef25099d66867c3b23e18399ed27
Author: rajputsher <shersingh72@gmail.com>
Date:   Tue Mar 16 20:38:20 2019 +0100

    replaced all contacts ending with 4315 with 4314

 4_explore_california/contact.html                    | 4 ++--
 4_explore_california/explorers.html                  | 2 +-
 4_explore_california/index.html                      | 2 +-
 4_explore_california/mission.html                    | 2 +-
 4_explore_california/resources.html                  | 2 +-
 4_explore_california/resources/faq.html              | 2 +-
 4_explore_california/support.html                    | 4 ++--
 4_explore_california/tours.html                      | 2 +-
 4_explore_california/tours/tour_detail_backpack.html | 2 +-
 4_explore_california/tours/tour_detail_bigsur.html   | 2 +-
 10 files changed, 12 insertions(+), 12 deletions(-)
```

- `git log --format=short`. --format = oneline|short|medium(default)|full|fuller|email|raw.Ex"
```
git log --format=raw

commit 4339bfba5ae73e98ab4a8133c9ede70154e12640
tree 459674b443dd829913d96202a5d14c9c54b71700
parent b961c181631e4581049bc6887b829b1047bd9ccd
author rajputsher <shersingh72@gmail.com> 1616336550 +0100
committer rajputsher <shersingh72@gmail.com> 1616336550 +0100

    Change folder name from 6_gitignore to 6_git_ignore

commit b961c181631e4581049bc6887b829b1047bd9ccd
tree 15f9d2f3762ef3807d9818ff0aef4f6d352fab92
parent d30be48ad6b338484eef01a19cda43ef4e6352a8
author rajputsher <shersingh72@gmail.com> 1616184189 +0100
committer rajputsher <shersingh72@gmail.com> 1616184189 +0100

    remove untracked files
```
- `git log --oneline`: to reduce the number of characters of SHA.
- `git log --graph` : Use full when there are branches and merges in the tree.
- `git log --graph --all --oneline --decorate`

```
git log --graph --all --oneline --decorate
*   63477f0 (HEAD -> master, origin/master, origin/HEAD) Merge branch 'document15032021'
|\
| * cbb3b3d (origin/document15032021) Updated Readme
* | 4950659 Handling thread join when exception is thrown
|/
*   61d0a85 Merge branch 'document'
|\
| * efd3332 (origin/document) Join and Detach
* | b5eb414 Join and Detach functions
|/
* 18f26de Joinability of threads
* 2692eb5 Launching a thread
* 2437b1b Parallelism and Concurrency
* bd685b4 Updated Readme
* 0b9f537 Intro
```

