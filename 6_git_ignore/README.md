## .gitignore files

- add .gitignore file in the root project folder.
- list the rules to determine which files to ignore
- Changes made to those files will be ignored by git.

What can be in the .gitignore files:

1. Pattern matching (Basic regular expression): *?[aeiou][0-9]

ex: logs/*.txt : ignores all .txt files in the log folder.

2. Negative expressions 

ex: *.php - ignore all .php files

!index.php - except for index.php file.

3. Ignore all files in a directory with a trailing slash

ex: assets/videos/ - will ignore everything in this folder

4. Comments : we can add comments in the .gitignore file with #.

ex: # This is a comment

## What to ignore

Github has a collection of useful .gitignore templates.
[Gitignore templates](https://github.com/github/gitignore) for different kind of projects.


## Globally ignore files 

`git config --global core.excludesfile ~/.gitignore_global` "~/.gitignore_global" can be any file.

## Ignore tracked files

`git rm --cached <filename>`

## Track empty directories

Git does not track empty directories. If you want to track the empty directory, add a empty file .gitkeep which is an invisible file.

