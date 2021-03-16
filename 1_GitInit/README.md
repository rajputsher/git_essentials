# Initialize a repository

`git init` : This creates .git folder in the parent folder . This is the folder where git stores all the versioning information, configuration etc.

Ex: .git/config file contains the configuration of the project. This is where project level configuration can be made.

Ig .git folder is where all the tracking is happening. If this folder is deleted, then the contents are no more tracked for versioning.


## Commit the changes

`git add .`: First add the files that you want to commit, or use `.` to indicate commit all the changes.

`git commit -m "Message summarizing the commit"`: This command is used to commit the changes with a message. `-m` is message .

The Main steps in git are :
1. Make Changes
2. Add the Changes: `git add .`
3. Commit changes to the repository with a message: `git commit -m "message"`


## Commit message best practices 

- A Short single-line summary(less than 50 characters)
- Optionally followed by a blank line and a more complete description
- Keep each line to less than 72 characters 
- Write commit messages in present tense, not past tense. "Fix of a bug" or "Fixes a bug", not "Fixed a bug"
- Bullet points are ususally asteriks or hyphens
- Can add "tracking numbers" from bugs or support requests
- Can develop shorthand specific to organization ex: "bugfix", "new feature", "requirement ID:" etc.

## View the commit log

`git log` : this command gives the history of log and commit ID. commit ID is unique.

The log message looks like : 

```
commit 0615242dac44a1760880fe571a4f9c06dde111d2 (HEAD -> master)
Author: rajputsher <shersingh72@gmail.com>
Date:   Tue Mar 16 08:27:32 2019 +0100

    Message description
```

Variations of log command :
- `git log -n 5`: Log of 5 recent commits
- `git log --since=2019-02-15` : Log since a specfic date
- `git log --until=2019-02-15`: Log until a specific date 
- `git log --author="Name/Partof the name"` 
- `git log --grep="Init"`: Returns all log with init in the commit message


Example: 
Output the log for all of Karen's commits labeled "refactor" during March 2019
```
git log --since=2019-03-01 --until=2019-03-31 --author="Karen" --grep="refactor"
```

## Set username/email for a specific repository

```git
git config user.name "Your project specific name"
git config user.email "your@project-specific-email.com"
```

Verify your settings: 

```git
git config --get user.name
git config --get user.email
```

## Set username/email globally

## Set username/email for a specific repository

```git
git config --global user.name "Your global username"
git config --global user.email "your@email.com"
```

Verify your settings: 

```git
git config --global --get user.name
git config --global --get user.email
```