#### Created: 2024-09-01
#### Tags: [[Git]] [[Version Control]] [[Development]]
#### Links: [[GitLab]] [[GitHub]] [[Branching Strategies]]

# Git Cheat Sheet

## Overview
This cheat sheet provides a quick reference for common Git commands and workflows. It's designed to help you navigate daily tasks in your Git-based projects.

## Basic Commands

### Setup and Configuration
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@company.com"
git config --list  # View all settings
```

### Creating Repositories
```bash
git init  # Initialize a new local repository
git clone <repository-url>  # Clone a remote repository
```

### Basic Snapshotting
```bash
git status  # Check status
git add <file>  # Add a file to staging area
git add .  # Add all changed files to staging area
git commit -m "Commit message"  # Commit changes
git commit -am "Commit message"  # Add changed files and commit
```

### Branching and Merging
```bash
git branch  # List branches (* denotes current branch)
git branch <branch-name>  # Create a new branch
git checkout <branch-name>  # Switch to a branch
git checkout -b <branch-name>  # Create and switch to a new branch
git merge <branch-name>  # Merge a branch into the current branch
git branch -d <branch-name>  # Delete a branch
```

### Sharing and Updating
```bash
git push origin <branch-name>  # Push branch to remote
git pull  # Fetch and merge changes from remote
git fetch  # Fetch changes from remote
```

## Advanced Commands

### Stashing
```bash
git stash  # Stash changes
git stash list  # List stashes
git stash apply  # Apply last stash
git stash pop  # Apply last stash and remove it from stash list
```

### Inspection and Comparison
```bash
git log  # View commit history
git log --oneline  # Compact view of commit history
git diff  # Show changes between working directory and staging area
git diff --staged  # Show changes between staging area and last commit
```

### Undoing Changes
```bash
git reset <file>  # Unstage a file
git checkout -- <file>  # Discard changes in working directory
git revert <commit>  # Create new commit that undoes specified commit
git reset --hard <commit>  # Reset to a previous commit (caution: destroys history)
```

### Remote Repositories
```bash
git remote -v  # List remote repositories
git remote add <name> <url>  # Add a remote repository
git push -u <remote> <branch>  # Push and set upstream branch
```

## Common Workflows

### Feature Branch Workflow
1. Create a feature branch:
   ```bash
   git checkout -b feature-branch
   ```
2. Make changes and commit:
   ```bash
   git add .
   git commit -m "Implement feature"
   ```
3. Push feature branch to remote:
   ```bash
   git push -u origin feature-branch
   ```
4. Create a merge request (in GitLab UI)
5. After approval, merge in UI or locally:
   ```bash
   git checkout main
   git pull
   git merge feature-branch
   git push
   ```

### Handling Merge Conflicts
1. Pull latest changes:
   ```bash
   git pull
   ```
2. If conflicts occur, resolve them in your editor
3. Stage resolved files:
   ```bash
   git add <resolved-file>
   ```
4. Complete the merge:
   ```bash
   git commit
   ```

## Best Practices
- Commit often with clear, descriptive messages
- Pull changes from the remote repository before starting new work
- Use branches for new features or bug fixes
- Review changes before committing (use `git diff`)
- Don't commit sensitive information or large binary files

## Common Pitfalls
- Forgetting to pull before starting new work
- Committing to the wrong branch
- Pushing sensitive information to a public repository
- Using `git reset --hard` without understanding its implications

## Additional Notes
Remember to consult your team's specific Git workflow and conventions, as they may have particular preferences or requirements for branching, commit messages, and merge processes.