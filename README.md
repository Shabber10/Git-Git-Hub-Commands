# Git & GitHub Command Guide (Basic, Medium & Advanced)

A structured, production-grade reference manual for mastering version control with **Git** (local) and cloud collaboration with **GitHub** (remote, CI/CD, and CLI), tiered by difficulty level.

---

## 💡 Git vs. GitHub: Quick Comparison

| Feature | Git | GitHub |
| :--- | :--- | :--- |
| **What it is** | Distributed Version Control System (VCS). | Cloud-based hosting & DevOps collaboration platform. |
| **Where it runs** | Locally on your computer (offline-capable). | In the cloud / on web servers (requires internet). |
| **Primary purpose** | Tracks history, records changes, manages branches & rebases. | Hosts repositories, handles PRs, Issues, CI/CD, and team governance. |
| **Interface** | Command Line Interface (CLI) & desktop clients. | Web UI, GitHub Desktop, GitHub CLI (`gh`), and APIs. |

---

## 📁 Repository Structure & Tiered Roadmap

```text
.
├── README.md
├── git-local-commands/
│   └── README.md          # Local Git operations (Basic ➔ Medium ➔ Advanced)
└── github-cloud-commands/
    └── README.md          # GitHub Cloud & CI/CD (Basic ➔ Medium ➔ Advanced)
```

---

## 🧭 Tiered Learning Paths

### 📦 [1. Local Git Commands](git-local-commands/README.md)
- 🟢 **Tier 1: Basic (Foundations & Daily Essentials)**
  - `git init`, `git config` — Setup & configuration
  - `git status`, `git add`, `git commit` — Staging and snapshots
  - `git log`, `git diff`, `git show` — History inspection
  - `git rm`, `git mv`, `.gitignore` — File management and exclusion rules
- 🟡 **Tier 2: Medium (Branching, Merging & Undoing)**
  - `git branch`, `git switch` / `git checkout` — Branch management
  - `git merge`, `git stash` — Integration and dirty-tree shelving
  - `git restore`, `git revert`, `git reset` (`--soft`/`--hard`) — Undoing mistakes
  - `git tag`, `.gitattributes` — Version marks and OS line-ending normalization
- 🔴 **Tier 3: Advanced (Power User, Internals & Forensics)**
  - `git rebase`, `git rebase -i`, `git cherry-pick` — History rewriting & squashing
  - `git reflog`, `git blame`, `git bisect` — Data recovery and binary bug search
  - `git worktree`, `git submodule` — Concurrent directories and nested repositories
  - `git clean`, `git archive`, `git gc`, `git fsck` — Housekeeping and object integrity

---

### ☁️ [2. GitHub Cloud Commands](github-cloud-commands/README.md)
- 🟢 **Tier 1: Basic (Remote Syncing & Tracking)**
  - `git clone`, `git remote add`, `git remote -v` — Connecting to cloud repos
  - `git fetch`, `git pull`, `git push`, `git branch -r` — Daily sync and tracking
- 🟡 **Tier 2: Medium (Collaboration, SSH & CLI Tools)**
  - SSH Key Authentication (`ssh-keygen`, `ssh-agent`, `ssh -T`) — Passwordless login
  - Full CLI Pull Request (PR) Lifecycle — Branching, pushing, and review flows
  - `git push --tags` — Publishing version tags
  - `gh auth login`, `gh repo create/clone/fork` — GitHub CLI fundamentals
- 🔴 **Tier 3: Advanced (DevOps, CI/CD & Governance)**
  - `gh pr` (`create`/`checkout`/`review`/`merge`) — Browserless PR management
  - `gh issue` (`create`/`list`/`close`) — Issue tracking from terminal
  - `gh release create` — Packaging releases with attached binaries
  - `gh workflow` & `gh run` — Triggering and debugging GitHub Actions CI/CD runs
  - `.github/CODEOWNERS`, Branch Protection, `.github/workflows/ci.yml` — DevOps governance

---

## 🚀 Quick Setup for Beginners

### 1. Install Tools
```bash
# Windows (PowerShell)
winget install --id Git.Git -e --source winget
winget install --id GitHub.cli -e --source winget

# macOS
brew install git gh

# Linux (Ubuntu/Debian)
sudo apt update && sudo apt install git gh -y
```

### 2. Configure Global Identity
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
git config --global init.defaultBranch main
```

### 3. Authenticate GitHub CLI
```bash
gh auth login
```
