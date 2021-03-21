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

