## Git Command Cheat Sheet

### Basic Commands

- Initialize a new Git repository `git init`
- Clone a repository `git clone`
- Check the status of a repository `git status`
- Add changes to the staging area:
  - `git add <file-name>` # Add a specific file
  - `git add .` # Add all changes

### Branching and Merging

- Create a new branch `git branch <branch-name>`
- Switch to a branch `git checkout <branch-name>`
- Create and Switch to a new branch `git checkout -b <branc-name>`
- Merge a branch into current branch `git merge <branch-name>`
- Delete a branch:
  - `git branch -d <branch-name>` # Delete a local branch
  - `git push origin --delete <branch-name>` # Delete a remote branch

### Remote Repository

- View Remote Repositories `git remote -v`
- Add a remote repository `git remote add <name> <repository-url>`
- Fetch Changes from Remote `git fetch <remote-name>`
- Pull Changes from Remote `git pull <remote-name> <branch-name>`
- Push Changes to Remote `git push <remote-name> <branch-name>`

### Undoing Changes

- Unstage a Staged File `git reset <file-name>`
- Revert a Commit `git revert <commit-hash>`
- Reset to Last Commit `git reset --hard HEAD`
- View commit history `git log`

### Helpful Tips

- Show changes made

  - `git diff ` # Show changes not staged
  - `git diff --cached ` # Show changes staged for commit

- Stash Changes
  - `git stash ` # Stash current changes
  - `git stash pop ` # Apply stashed changes
- Tagging
  `git tag <tag-name>  ` # Create a tag
  `git push origin <tag-name>` # Push a tag to remote
