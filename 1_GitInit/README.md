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