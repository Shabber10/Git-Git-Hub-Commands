# Local Git Commands: Basic, Medium & Advanced

A structured, high-density reference sheet categorized by mastery levels—from essential day-to-day basics to intermediate branching and advanced repository forensics.

---

## 🟢 TIER 1: BASIC (Foundations & Daily Essentials)

Commands every developer uses daily to initialize repositories, stage changes, record snapshots, and inspect working history.

### 1. Setup & Configuration

#### `git init`
- **Explanation:** Initializes a brand new, empty Git repository inside the target directory by creating a `.git` metadata folder.
- **Syntax:** `git init [project-name]`
- **Example:**
  ```bash
  # Initialize repo in current folder
  git init

  # Initialize repo in a new subfolder
  git init api-service
  ```

#### `git config`
- **Explanation:** Sets configuration variables controlling user identity, repository behavior, and global defaults.
- **Syntax:** `git config [--global|--local|--system] <key> "<value>"`
- **Example:**
  ```bash
  git config --global user.name "Jane Doe"
  git config --global user.email "jane@example.com"
  ```

---

### 2. Saving Changes (Working Tree & Staging)

#### `git status`
- **Explanation:** Displays the state of the working directory and staging area, highlighting tracked and untracked modifications.
- **Syntax:** `git status [-s|--short]`
- **Example:**
  ```bash
  git status -s
  ```

#### `git add`
- **Explanation:** Moves modified and new files from the working directory into the staging area (index) for the next commit.
- **Syntax:** `git add <file-path> | . | -A`
- **Example:**
  ```bash
  # Stage single file
  git add src/app.js

  # Stage all changes
  git add -A
  ```

#### `git commit`
- **Explanation:** Records a permanent snapshot of staged changes into project history with a descriptive message.
- **Syntax:** `git commit -m "<message>" [-a]`
- **Example:**
  ```bash
  # Commit staged changes
  git commit -m "feat(auth): implement JWT token verification"

  # Stage tracked files and commit in one step
  git commit -am "fix(nav): resolve mobile dropdown bug"
  ```

---

### 3. History & Inspection

#### `git log`
- **Explanation:** Lists the commit history in reverse chronological order for the current branch.
- **Syntax:** `git log [--oneline] [--graph] [--decorate] [-n <count>]`
- **Example:**
  ```bash
  git log --oneline --graph --all -n 10
  ```

#### `git diff`
- **Explanation:** Compares and displays line-by-line differences between the working tree, staging area, or commits.
- **Syntax:** `git diff [<commit>] [--staged] [<file>]`
- **Example:**
  ```bash
  # View unstaged changes
  git diff

  # View staged changes
  git diff --staged
  ```

#### `git show`
- **Explanation:** Displays the commit metadata, author details, and diff for a specific commit hash or object.
- **Syntax:** `git show [<commit-hash>|HEAD]`
- **Example:**
  ```bash
  git show HEAD
  ```

---

### 4. Basic File Operations & Ignore Rules

#### `git rm`
- **Explanation:** Removes files from both disk and the Git staging index (or un-tracks without deleting from disk).
- **Syntax:** `git rm [-f] [--cached] <file-path>`
- **Example:**
  ```bash
  # Stop tracking .env without deleting from local disk
  git rm --cached .env
  ```

#### `git mv`
- **Explanation:** Renames or moves a file and automatically stages the change.
- **Syntax:** `git mv <source> <destination>`
- **Example:**
  ```bash
  git mv server.js app.js
  ```

#### `.gitignore` Configuration
- **Explanation:** Plaintext file telling Git which files and directories to ignore and never track.
- **Example:**
  ```gitignore
  node_modules/
  .env
  dist/
  *.log
  ```

---

## 🟡 TIER 2: MEDIUM (Branching, Merging & Undoing)

Commands and workflows needed for feature development, isolated experimentation, resolving mistakes, and team integration.

### 1. Branch Management & Switching

#### `git branch`
- **Explanation:** Lists, creates, renames, or deletes local branches.
- **Syntax:** `git branch [-a] [-d|-D <branch-name>] [<new-branch>]`
- **Example:**
  ```bash
  # List branches
  git branch

  # Safely delete merged branch
  git branch -d feature/login
  ```

#### `git checkout` / `git switch`
- **Explanation:** Switches between branches or checks out specific commits (modern Git recommends `git switch`).
- **Syntax:** `git switch <branch-name> | -c <new-branch>`
- **Example:**
  ```bash
  # Create and switch to new branch
  git switch -c feature/payment-gateway
  ```

---

### 2. Merging & Stashing

#### `git merge`
- **Explanation:** Merges history from another branch into the currently active branch.
- **Syntax:** `git merge <source-branch> [--no-ff]`
- **Example:**
  ```bash
  git switch main
  git merge feature/payment-gateway
  ```

#### `git stash`
- **Explanation:** Temporarily saves dirty working tree changes without committing, giving you a clean slate.
- **Syntax:** `git stash [push -m "<msg>"|pop|list|drop|apply]`
- **Example:**
  ```bash
  # Stash current work with message
  git stash push -m "WIP: cart checkout logic"

  # Pop changes back when ready
  git stash pop
  ```

---

### 3. Undoing Mistakes Safely

#### `git checkout -- <file>` / `git restore <file>`
- **Explanation:** Discards uncommitted modifications in a specific file, resetting it back to `HEAD`.
- **Syntax:** `git restore <file-path>`
- **Example:**
  ```bash
  git restore src/config.json
  ```

#### `git revert`
- **Explanation:** Creates a new commit that inverts the changes of a prior commit, safely rolling back changes in public branches.
- **Syntax:** `git revert <commit-hash> [--no-edit]`
- **Example:**
  ```bash
  git revert a1b2c3d
  ```

#### `git reset`
- **Explanation:** Rewinds current `HEAD` to an older commit with options to keep or discard working tree changes.
- **Syntax:** `git reset [--soft|--mixed|--hard] <commit>`
- **Example:**
  ```bash
  # Soft reset: moves HEAD, keeps changes staged
  git reset --soft HEAD~1

  # Hard reset: permanently discards all changes (destructive)
  git reset --hard HEAD~1
  ```

---

### 4. Tagging & File Attributes

#### `git tag`
- **Explanation:** Marks a specific commit in history with a human-readable release version tag.
- **Syntax:** `git tag [-a <tag-name> -m "<msg>"]`
- **Example:**
  ```bash
  git tag -a v1.0.0 -m "Release version 1.0.0"
  ```

#### `.gitattributes`
- **Explanation:** Configures repository path attributes such as line ending normalization (`LF`/`CRLF`) and binary designations.
- **Example:**
  ```gitattributes
  * text=auto eol=lf
  *.bat text eol=crlf
  *.png binary
  ```

---

## 🔴 TIER 3: ADVANCED (Power User, Internals & Forensics)

Commands used by senior engineers for history rewriting, bug hunting, multiple worktrees, submodules, and low-level repository optimization.

### 1. History Rewriting & Selective Commits

#### `git rebase` (Standard & Interactive)
- **Explanation:** Reapplies commits from your branch on top of another base to maintain a clean linear history, or rewrite past commits interactively.
- **Syntax:**
  ```bash
  git rebase <base-branch>
  git rebase -i <commit-hash>
  ```
- **Example:**
  ```bash
  # Rebase on main
  git rebase main

  # Interactive rebase of last 4 commits (squash/reword/edit/drop)
  git rebase -i HEAD~4
  ```

#### `git cherry-pick`
- **Explanation:** Applies the changes introduced by an existing commit from another branch directly onto your active branch.
- **Syntax:** `git cherry-pick <commit-hash> [--no-commit]`
- **Example:**
  ```bash
  git cherry-pick f8c9b2a
  ```

---

### 2. Recovery & Debugging Forensics

#### `git reflog`
- **Explanation:** Records every movement of `HEAD` and branch references, providing a recovery safety net for lost commits or deleted branches.
- **Syntax:** `git reflog [show]`
- **Example:**
  ```bash
  # View reflog history
  git reflog

  # Restore lost commit
  git reset --hard HEAD@{2}
  ```

#### `git blame`
- **Explanation:** Shows the commit hash, author, and timestamp for each line in a file to inspect historical modifications.
- **Syntax:** `git blame [-L <start>,<end>] <file-path>`
- **Example:**
  ```bash
  git blame -L 15,30 src/services/auth.ts
  ```

#### `git bisect`
- **Explanation:** Performs an automated binary search through commit history to quickly find the exact commit that introduced a bug.
- **Syntax:** `git bisect [start|bad|good|reset]`
- **Example:**
  ```bash
  git bisect start
  git bisect bad              # Current commit is broken
  git bisect good v1.1.0      # v1.1.0 was working
  # Test intermediate commits prompted by Git, then:
  git bisect reset
  ```

---

### 3. Advanced Workspaces & Modularity

#### `git worktree`
- **Explanation:** Manages multiple working directories linked to the same repository, allowing simultaneous work on multiple branches without switching folders.
- **Syntax:** `git worktree [add|list|remove] <path> [<branch>]`
- **Example:**
  ```bash
  # Check out a hotfix branch in a separate folder
  git worktree add ../hotfix hotfix/critical-patch

  # Remove worktree when done
  git worktree remove ../hotfix
  ```

#### `git submodule`
- **Explanation:** Keeps an external Git repository as a tracked subdirectory within another parent Git repository.
- **Syntax:** `git submodule [add|init|update] <repo-url> [<path>]`
- **Example:**
  ```bash
  git submodule add https://github.com/org/core-lib.git libs/core
  git submodule update --init --recursive
  ```

---

### 4. Maintenance & Exports

#### `git clean`
- **Explanation:** Cleans untracked files and directories out of the working tree.
- **Syntax:** `git clean [-n] [-f] [-d]`
- **Example:**
  ```bash
  # Dry-run preview
  git clean -nd

  # Force clean untracked files and folders
  git clean -fd
  ```

#### `git archive`
- **Explanation:** Packages files from a commit or branch into a clean `.zip` or `.tar` archive without the `.git` folder.
- **Syntax:** `git archive --format=<zip|tar> --output=<filename> <branch>`
- **Example:**
  ```bash
  git archive --format=zip --output=release-v1.0.zip main
  ```

#### `git gc` & `git fsck`
- **Explanation:** Optimizes repository performance by packing objects (`git gc`) and validates the integrity of the Git object store (`git fsck`).
- **Syntax:**
  ```bash
  git gc --prune=now
  git fsck --full
  ```
