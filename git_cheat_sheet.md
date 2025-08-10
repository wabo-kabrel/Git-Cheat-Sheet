# Git Cheat Sheet — From Beginner to Expert

---

## 1. Setup & Configuration

```bash
git --version                  # Check Git version
git config --global user.name "Your Name"     # Set username
git config --global user.email "you@example.com"  # Set email
git config --list              # View current config
```


## 2. Creating & Initializing Repositories
```bash
git init                      # Initialize new repo locally
git clone <repo_url>          # Clone existing repo  
```


## 3. Basic Workflow
``` bash
git status                   # Check repo status
git add <file(s)>            # Stage files for commit
git commit -m "message"      # Commit staged changes
git log                      # Show commit history
git log --oneline            # Compact log
```


## 4. Branching & Merging
``` bash
git branch                   # List branches
git branch <branch_name>     # Create branch
git checkout <branch_name>   # Switch branches
git checkout -b <branch>     # Create and switch branch
git merge <branch>           # Merge branch into current
```


## 5. Remote Repositories
```bash
git remote add origin <url>  # Add remote repo
git remote -v                # List remotes
git fetch                    # Fetch changes without merge
git pull                     # Fetch and merge changes
git push origin <branch>     # Push commits to remote branch
```


## 6. Tracking Branches
``` bash
git branch --set-upstream-to=origin/main main   # Link local to remote
git push --set-upstream origin <branch>         # Push and track branch
```


## 7. Rebasing
```bash
git rebase <branch>          # Rebase current branch onto <branch>
git rebase -i HEAD~3         # Interactive rebase last 3 commits (edit, squash, reorder)
git push --force-with-lease  # Force push safely after rebase
```


## 8. Stashing
```bash
git stash                   # Save uncommitted changes
git stash push -m "msg"     # Save stash with message
git stash list              # List stashes
git stash apply stash@{0}   # Apply stash without removing
git stash pop               # Apply stash and remove it
git stash drop stash@{0}    # Remove stash

```


## 9. Cherry-picking & Reflog
```bash
git cherry-pick <commit>   # Apply specific commit to current branch
git reflog                 # Show history of HEAD movements
git reset --hard <commit>  # Reset working tree to a commit
```


## 10. Submodules
```bash
git submodule add <url> <path>           # Add submodule
git submodule update --init --recursive  # Initialize submodules
git submodule foreach git pull           # Update submodules
```


## 11. Git Hooks (Automation)
Hooks are scripts inside .git/hooks/ directory.
Common hooks:
- pre-commit: Run tests or lint before commit
- commit-msg: Validate commit messages
 
Make hooks executable (chmod +x).
Example pre-commit hook to block commits containing TODO:

```sh
#!/bin/sh
if git diff --cached | grep -q TODO; then
    echo "Commit aborted: TODO found"
    exit 1
fi
```


## 12. Handling Merge Conflicts
- Conflicts occur when changes overlap between branches.
* Resolve manually or with git mergetool.
+ After fixing, stage and commit.
```bash
git merge <branch>
# Resolve conflicts in files
git add <resolved_files>
git commit
```


## 13. Multiple Remotes
```bash
git remote add upstream <url>    # Add additional remote (e.g., original repo)
git fetch upstream               # Fetch changes from upstream
git pull upstream main           # Pull changes from upstream main branch
```


## 14. Best Practices
- Commit early and often with meaningful messages
- Use branches for features/fixes
- Regularly pull/fetch updates
- Avoid rebasing shared branches without coordination
- Use .gitignore to exclude unnecessary files
- Use git stash to save work in progress
- Keep pull requests small and focused


## 15. Useful Miscellaneous Commands
```bash
git diff                  # Show changes not staged
git diff --staged         # Show staged changes
git show <commit>         # Show details of a commit
git reset HEAD <file>     # Unstage a file
git clean -f              # Remove untracked files
git tag <tagname>         # Create a tag
git push origin --tags    # Push tags to remote
```


## 16. Collaboration Workflow (GitHub Flow example)
1. Create a feature branch off main.
2. Commit your changes locally.
3. Push branch to remote.
4. Open a Pull Request (PR) for review.
5. After review and CI checks, merge to main.
6. Pull latest main locally and continue work.
