# Local Git Commands Guide

A dense, high-impact reference sheet for managing repositories, version history, debugging, and advanced workflows on your local machine.

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

---

## 🔀 6. Advanced History & Branch Manipulation

### `git rebase`
- **Explanation:** Reapplies commits from the current branch on top of another base tip to maintain a clean, linear commit history.
- **Syntax:**
  ```bash
  git rebase <base-branch>
  git rebase -i <commit-reference>
  ```
- **Example:**
  ```bash
  # Rebase current feature branch on top of latest main
  git rebase main

  # Interactive rebase of the last 4 commits (squash, edit, reword, drop)
  git rebase -i HEAD~4
  ```

### `git cherry-pick`
- **Explanation:** Applies the changes introduced by one or more existing commits from another branch onto your currently checked-out branch.
- **Syntax:**
  ```bash
  git cherry-pick <commit-hash> [--no-commit]
  ```
- **Example:**
  ```bash
  # Apply a specific hotfix commit from 'main' into 'release-v1.0'
  git cherry-pick d3e4f5a
  ```

### `git reflog`
- **Explanation:** Records every single update made to tip of branches and `HEAD`, providing a safety net to recover deleted branches or lost commits.
- **Syntax:**
  ```bash
  git reflog [show]
  ```
- **Example:**
  ```bash
  # Inspect history of HEAD movements to find a lost commit hash
  git reflog

  # Restore state to a previous point in reflog
  git reset --hard HEAD@{3}
  ```

---

## 🔬 7. Debugging & Forensics

### `git blame`
- **Explanation:** Annotates each line in a file with the commit ID, author, and timestamp of the last edit.
- **Syntax:**
  ```bash
  git blame [-L <start>,<end>] <file-path>
  ```
- **Example:**
  ```bash
  # Inspect who modified lines 20 through 45 in server.ts
  git blame -L 20,45 server.ts
  ```

### `git bisect`
- **Explanation:** Uses binary search across commit history to rapidly pinpoint the exact commit that introduced a bug or regression.
- **Syntax:**
  ```bash
  git bisect [start|bad|good|reset]
  ```
- **Example:**
  ```bash
  # Start bisect session
  git bisect start

  # Mark current HEAD as broken/bad
  git bisect bad

  # Mark a known working commit/tag as good
  git bisect good v1.2.0

  # Git checks out intermediate commits for testing; when done, terminate session:
  git bisect reset
  ```

---

## 🗃️ 8. File & Working Tree Operations

### `git rm`
- **Explanation:** Removes files from both the working directory and the staging area index (or index only).
- **Syntax:**
  ```bash
  git rm [-f] [--cached] <file-path>
  ```
- **Example:**
  ```bash
  # Remove file from disk and stage removal
  git rm old_module.js

  # Stop tracking a file without deleting it from disk (e.g. .env)
  git rm --cached .env
  ```

### `git mv`
- **Explanation:** Moves or renames a file, directory, or symlink and stages the change automatically.
- **Syntax:**
  ```bash
  git mv <source> <destination>
  ```
- **Example:**
  ```bash
  # Rename a file cleanly while preserving history
  git mv utils.js helpers.js
  ```

### `git clean`
- **Explanation:** Removes untracked files and directories from the working tree to restore a clean state.
- **Syntax:**
  ```bash
  git clean [-n] [-f] [-d]
  ```
- **Example:**
  ```bash
  # Dry-run: preview untracked files that will be deleted
  git clean -nd

  # Force delete all untracked files and directories
  git clean -fd
  ```

---

## 🏷️ 9. Tags & Version Releases

### `git tag`
- **Explanation:** Creates, lists, verifies, or deletes specific points in history as release tags (lightweight or annotated).
- **Syntax:**
  ```bash
  git tag [-a <tag-name> -m "<message>"] [-d <tag-name>]
  ```
- **Example:**
  ```bash
  # Create an annotated release tag with a message
  git tag -a v1.0.0 -m "Release version 1.0.0: Initial stable release"

  # List all existing tags
  git tag -l

  # Delete a local tag
  git tag -d v0.9.0-beta
  ```

---

## 🏢 10. Advanced Workflows: Worktrees & Submodules

### `git worktree`
- **Explanation:** Manages multiple working trees attached to the same repository, allowing you to check out multiple branches simultaneously in separate folders.
- **Syntax:**
  ```bash
  git worktree [add|list|remove|prune] <path> [<branch>]
  ```
- **Example:**
  ```bash
  # Check out a hotfix branch into a separate parallel directory without switching context
  git worktree add ../hotfix-dir hotfix/security-patch

  # List active worktrees
  git worktree list

  # Remove a worktree directory when finished
  git worktree remove ../hotfix-dir
  ```

### `git submodule`
- **Explanation:** Incorporates and tracks external Git repositories as subdirectories inside your main repository.
- **Syntax:**
  ```bash
  git submodule [add|init|update|status] <repository-url> [<path>]
  ```
- **Example:**
  ```bash
  # Add an external shared library repository as a submodule
  git submodule add https://github.com/org/shared-lib.git libs/shared

  # Initialize and clone submodules after pulling parent repo
  git submodule update --init --recursive
  ```

---

## 🧹 11. Maintenance & Internals

### `git archive`
- **Explanation:** Creates a clean zip or tarball archive containing files from a named commit or branch without Git metadata (`.git`).
- **Syntax:**
  ```bash
  git archive --format=<zip|tar> --output=<filename> <branch|tag>
  ```
- **Example:**
  ```bash
  # Export release snapshot as a ZIP file
  git archive --format=zip --output=release-v1.0.0.zip main
  ```

### `git gc` & `git fsck`
- **Explanation:** Optimizes repository performance by packing objects (`git gc`) and verifies the data integrity of the internal object database (`git fsck`).
- **Syntax:**
  ```bash
  git gc [--prune=<date>]
  git fsck [--full]
  ```
- **Example:**
  ```bash
  # Clean up loose objects and optimize repository size
  git gc --prune=now

  # Verify internal object database integrity
  git fsck --full
  ```

---

## 📄 12. Repository Configuration Files

### `.gitignore`
Controls files and patterns that Git intentionally ignores and will never track.
- **Example `.gitignore` pattern file:**
  ```gitignore
  # Dependencies
  node_modules/
  __pycache__/
  venv/

  # Environment secrets & credentials
  .env
  *.pem
  *.key

  # OS and IDE files
  .DS_Store
  Thumbs.db
  .vscode/
  .idea/

  # Build outputs
  dist/
  build/
  *.log
  ```

### `.gitattributes`
Defines attributes on per-path basis (line-ending normalization across OSes, diff behavior for binary files, LFS tracking).
- **Example `.gitattributes` file:**
  ```gitattributes
  # Auto-normalize line endings to LF on commit
  * text=auto eol=lf

  # Force CRLF for Windows-specific batch scripts
  *.bat text eol=crlf

  # Treat images and archives as binary
  *.png binary
  *.jpg binary
  *.zip binary
  ```
