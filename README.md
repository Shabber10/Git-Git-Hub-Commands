# Complete Git & GitHub Command Guide

A production-grade reference manual for mastering version control with **Git** (local) and cloud collaboration with **GitHub** (remote, CI/CD, and GitHub CLI).

---

## 💡 Git vs. GitHub: What is the Difference?

| Feature | Git | GitHub |
| :--- | :--- | :--- |
| **What it is** | Distributed Version Control System (VCS) engine. | Cloud-based hosting, collaboration, and DevOps platform. |
| **Where it runs** | Locally on your computer (offline-capable). | In the cloud / on web servers (requires internet). |
| **Primary purpose** | Tracks history, records changes, manages branches & rebases. | Hosts repositories, handles PRs, Issues, CI/CD, and team governance. |
| **Interface** | Command Line Interface (CLI) & desktop clients. | Web UI, GitHub Desktop, GitHub CLI (`gh`), and APIs. |
| **Key Operations** | `init`, `commit`, `branch`, `rebase`, `bisect`, `stash`. | `pull`, `push`, `PRs`, `Actions (CI/CD)`, `Releases`, `Issues`. |

> **Key Takeaway:** Git is the engine that records your code history; GitHub is the platform where you share, automate, review, and govern that history with teams.

---

## 📁 Repository Structure

```text
.
├── README.md                          # Root directory overview & quick setup guide
├── git-local-commands/
│   └── README.md                      # Complete local Git operations & advanced workflows
└── github-cloud-commands/
    └── README.md                      # Remote GitHub operations, CI/CD, PRs & GitHub CLI
```

---

## 🧭 Navigation & Modules

### 📦 [Local Git Operations Guide](git-local-commands/README.md)
1. **Setup & Configuration:** `git init`, `git config`
2. **Saving Changes:** `git status`, `git add`, `git commit`
3. **History & Inspection:** `git log`, `git diff`, `git show`
4. **Branching & Merging:** `git branch`, `git checkout` / `git switch`, `git merge`, `git stash`
5. **Undoing Changes:** `git reset`, `git revert`, `git checkout -- <file>` / `git restore`
6. **Advanced History & Manipulation:** `git rebase` (interactive `-i`), `git cherry-pick`, `git reflog`
7. **Debugging & Forensics:** `git blame`, `git bisect`
8. **File & Working Tree Operations:** `git rm`, `git mv`, `git clean`
9. **Tags & Version Releases:** `git tag` (annotated & lightweight)
10. **Advanced Workflows:** `git worktree`, `git submodule`
11. **Maintenance & Internals:** `git archive`, `git gc`, `git fsck`
12. **Configuration Files:** `.gitignore`, `.gitattributes`

### ☁️ [GitHub Cloud Operations Guide](github-cloud-commands/README.md)
1. **Remote Syncing:** `git clone`, `git remote add`, `git remote -v`, `git fetch`, `git pull`, `git push`
2. **SSH Key Setup & Authentication:** `ssh-keygen`, `ssh-agent`, GitHub SSH keys, `ssh -T`
3. **Collaboration Workflows & PRs:** `git branch -r`, End-to-End Pull Request lifecycle
4. **Tags & Releases Distribution:** `git push --tags`, `gh release create`
5. **GitHub CLI (`gh`):** `gh auth login`, `gh repo create/clone/fork`, `gh issue`, `gh pr`
6. **CI/CD Automation:** `gh workflow list/run`, `gh run list/watch/view`
7. **Governance & DevOps Files:** `.github/CODEOWNERS`, Branch Protection Rules, `.github/workflows/ci.yml`

---

## 🚀 Quick Setup for Beginners

### Step 1: Install Git & GitHub CLI
- **Windows**:
  ```powershell
  winget install --id Git.Git -e --source winget
  winget install --id GitHub.cli -e --source winget
  ```
- **macOS**:
  ```bash
  brew install git gh
  ```
- **Linux (Ubuntu/Debian)**:
  ```bash
  sudo apt update && sudo apt install git gh -y
  ```

### Step 2: Configure Global Identity
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
git config --global init.defaultBranch main
```

### Step 3: Authenticate GitHub CLI
```bash
gh auth login
```
