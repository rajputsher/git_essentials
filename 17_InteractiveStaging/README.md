## Interactive Staging

- Stage changed interactively
- Allow staging portions of changed files
- Helps to make smaller, focused commits
- Feature of many git gui tools

Usage: 
- `git add --interactive`
- `git add -i`



## Patch mode

- Allows staging portions of a changed file.
- "Hunk": an area where two files differ
- Hunks can be staged, skipped or split into smaller hunks

We can go to patch mode by first entering the interactive mode with `git add -i` and follow the steps. OR with `git add --patch` or `git add -p`. 

