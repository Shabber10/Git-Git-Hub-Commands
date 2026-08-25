# Local Git Commands Guide

A dense, high-impact reference sheet for managing repositories and version history on your local machine.

---

## 🛠️ 1. Setup & Configuration

### `git init`
- **Explanation:** Initializes a brand new, empty Git repository inside the target directory by creating a `.git` metadata folder.
- **Syntax:**
  ```bash
  git init [project-name]
  ```
- **Example:**
  ```bash
  # Initialize a repository in the current folder
  git init

  # Initialize a repository inside a new subdirectory named 'api-service'
  git init api-service
  ```

### `git config`
- **Explanation:** Reads and sets configuration variables that control repository behavior, user identity, and aliases across system, global, and local scopes.
- **Syntax:**
  ```bash
  git config [--global|--local|--system] <key> "<value>"
  ```
- **Example:**
  ```bash
  # Set global committer name
  git config --global user.name "Jane Doe"

  # Set repository-specific email address
  git config --local user.email "jane@work.com"
  ```

---

## 💾 2. Saving Changes

### `git status`
- **Explanation:** Displays the working tree status, highlighting untracked, modified, and staged files.
- **Syntax:**
  ```bash
  git status [-s|--short]
  ```
- **Example:**
  ```bash
  # Standard detailed status
  git status

  # Compact output for quick terminal scans
  git status -s
  ```

### `git add`
- **Explanation:** Adds file modifications in the working directory to the staging area (index) in preparation for the next commit.
- **Syntax:**
  ```bash
  git add <file-path> | . | -A
  ```
- **Example:**
  ```bash
  # Stage a single file
  git add src/index.js

  # Stage all new, modified, and deleted files in the repository
  git add -A
  ```

### `git commit`
- **Explanation:** Records a permanent snapshot of the staged changes to the repository history with a descriptive log message.
- **Syntax:**
  ```bash
  git commit -m "<commit-message>" [-a]
  ```
- **Example:**
  ```bash
  # Commit staged changes with message
  git commit -m "feat(auth): add OAuth2 token validation"

  # Automatically stage modified tracked files and commit
  git commit -am "fix(router): handle 404 redirect edge case"
  ```

---

## 🔍 3. History & Inspection

### `git log`
- **Explanation:** Shows the commit history for the current branch in reverse chronological order.
- **Syntax:**
  ```bash
  git log [--oneline] [--graph] [--decorate] [-n <count>]
  ```
- **Example:**
  ```bash
  # Compact visual graph of recent commits
  git log --oneline --graph --all -n 10
  ```

### `git diff`
- **Explanation:** Displays line-by-line differences between the working tree, staging area, or separate commits.
- **Syntax:**
  ```bash
  git diff [<commit-a>] [<commit-b>] [--staged] [<file-path>]
  ```
- **Example:**
  ```bash
  # View unstaged changes in working directory
  git diff

  # View staged changes compared to the last commit (HEAD)
  git diff --staged
  ```

### `git show`
- **Explanation:** Inspects metadata and displays content changes for a specific commit hash, tag, or object.
- **Syntax:**
  ```bash
  git show [<object-id>]
  ```
- **Example:**
  ```bash
  # Show details of the latest commit
  git show HEAD

  # Show details and patch for a specific commit hash
  git show a1b2c3d
  ```

---

## 🌿 4. Branching & Merging

### `git branch`
- **Explanation:** Lists, creates, renames, or deletes branches in your local repository.
- **Syntax:**
  ```bash
  git branch [-a] [-d|-D <branch-name>] [<new-branch-name>]
  ```
- **Example:**
  ```bash
  # List all local branches
  git branch

  # Create a new branch named 'feature/login' without switching to it
  git branch feature/login

  # Safely delete a merged branch
  git branch -d feature/login
  ```

### `git checkout` / `git switch`
- **Explanation:** Updates files in the working tree to match the version in specified branches or commits (use `git switch` for branch transitions in modern Git).
- **Syntax:**
  ```bash
  git checkout <branch-name> | -b <new-branch-name>
  git switch <branch-name> | -c <new-branch-name>
  ```
- **Example:**
  ```bash
  # Switch to an existing branch (legacy checkout)
  git checkout main

  # Create and switch to a new branch (modern syntax)
  git switch -c feature/payment-gateway
  ```

### `git merge`
- **Explanation:** Joins two or more development histories together into the currently active branch.
- **Syntax:**
  ```bash
  git merge <source-branch> [--no-ff]
  ```
- **Example:**
  ```bash
  # Ensure you are on the target branch first
  git switch main

  # Merge 'feature/login' into 'main'
  git merge feature/login
  ```

### `git stash`
- **Explanation:** Temporarily shelves (stashes) uncommitted working directory changes so you can work on another task with a clean working copy.
- **Syntax:**
  ```bash
  git stash [push -m "<message>"|pop|list|drop|apply]
  ```
- **Example:**
  ```bash
  # Stash current modified and staged changes with a note
  git stash push -m "WIP: redesigning navigation bar"

  # Restore and remove the most recently stashed changes
  git stash pop
  ```

---

## ⏪ 5. Undoing Changes

### `git reset`
- **Explanation:** Resets current `HEAD` and optionally updates the staging area and working tree to a specified state.
- **Syntax:**
  ```bash
  git reset [--soft|--mixed|--hard] <commit-reference>
  ```
- **Example:**
  ```bash
  # Unstage files while keeping working directory modifications (mixed)
  git reset HEAD src/app.py

  # Move HEAD back 1 commit, keep changes staged (soft)
  git reset --soft HEAD~1

  # Discard ALL uncommitted changes and match HEAD (destructive)
  git reset --hard HEAD
  ```

### `git revert`
- **Explanation:** Creates a new commit that applies the exact inverse changes of a specified commit, safely preserving public history.
- **Syntax:**
  ```bash
  git revert <commit-hash> [--no-edit]
  ```
- **Example:**
  ```bash
  # Safely roll back changes introduced in commit 'a1b2c3d'
  git revert a1b2c3d
  ```

### `git checkout -- <file>` / `git restore <file>`
- **Explanation:** Discards local uncommitted changes in a specific file, restoring it to match the `HEAD` commit.
- **Syntax:**
  ```bash
  git checkout -- <file-path>     # Legacy syntax
  git restore <file-path>         # Modern syntax (Git 2.23+)
  ```
- **Example:**
  ```bash
  # Discard modifications in config.json (legacy)
  git checkout -- config.json

  # Discard modifications in config.json (modern)
  git restore config.json
  ```
