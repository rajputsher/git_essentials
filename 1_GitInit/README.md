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

git log


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