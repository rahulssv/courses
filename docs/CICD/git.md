# Git Commands
## Basic Concepts:
 
### Initialization and Configuration:
```bash
git init                             # Initialize a new Git repository
git config --global user.name "John Doe"
git config --global user.email "john.doe@example.com"
```
 
### Basic Workflow:
```bash
touch README.md # Create a new README.md file
git status                           # Check the status of the repository
git add README.md # Add README.md to the staging area
git commit -m "Add README.md"       # Commit changes with a message
git log                              # View commit history
```
 
### Branching and Merging:
```bash
git branch                          # List all branches
git branch feature                  # Create a new branch named 'feature'
git checkout feature                # Switch to the 'feature' branch
# Make changes, commit them
git checkout main                   # Switch back to the 'main' branch
git merge feature                   # Merge 'feature' branch into 'main'
```
 
### Remote Repositories:
```bash
git remote add origin <remote-repository-URL>  # Add a remote repository
git push -u origin main           # Push changes to the remote 'main' branch
git pull                           # Fetch and merge changes from the remote repository
git fetch                          # Fetch changes from the remote repository
```
 
### Collaboration:
```bash
git checkout -b my-feature         # Create and switch to a new branch in one command
# Make changes, commit them
git push origin my-feature         # Push changes to a new remote branch 'my-feature'
git pull origin main              # Pull changes from the 'main' branch of the remote repository
git push origin --delete old-feature  # Delete a remote branch named 'old-feature'
```
 
## Advanced Concepts:
 
### Rebasing:
```bash
git checkout my-feature
git rebase main                    # Rebase 'my-feature' onto the latest changes in the 'main' branch
```
 
### Stashing:
```bash
# Make changes to working directory
git stash                          # Stash changes in the working directory
# Work on something else
git stash apply                    # Apply the most recent stash
```
 
### Submodules:
```bash
git submodule add <submodule-URL> <path>  # Add a submodule to the repository
git submodule update --init        # Initialize and update submodules
```
 
### Cherry-picking:
```bash
git log                             # View commit history and find the commit to cherry-pick
git cherry-pick <commit-hash>      # Apply changes from a specific commit to the current branch
```
 
### Interactive Rebasing:
```bash
git rebase -i main                 # Interactively rebase to modify commits before applying them
# Squash, reword, edit, or drop commits as needed
```
 
### Reflog:
```bash
git reflog                         # View the reflog to recover lost commits or branches
git reset --hard HEAD@{n}          # Reset to a previous state based on the reflog
```
 
### Undoing Changes:
```bash
git reset HEAD file.txt            # Unstage changes for a file
git checkout -- file.txt           # Discard changes in the working directory for a file
git revert <commit-hash>           # Revert a commit, creating a new commit with the reverted changes
```
 
### Viewing Differences:
```bash
git diff                            # Show changes between the working directory and the staging area
git diff --cached                   # Show changes between the staging area and the repository
git diff <commit1> <commit2>        # Show changes between two commits
```
 
### Tagging:
```bash
git tag <tag-name>                  # Create a lightweight tag at the current commit
git tag -a <tag-name> -m "Tag message"  # Create an annotated tag with a message
git show <tag-name>                # Show information about a tag
```
 
### Gitignore:
```bash
touch .gitignore                    # Create a .gitignore file
# Add file patterns to ignore, such as '*.log' or 'node_modules/'
```