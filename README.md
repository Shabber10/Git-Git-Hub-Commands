# Git & GitHub Command Guide

A comprehensive, production-grade reference manual for mastering version control with **Git** (local) and cloud collaboration with **GitHub** (remote).

---

## 💡 Git vs. GitHub: What is the Difference?

| Feature | Git | GitHub |
| :--- | :--- | :--- |
| **What it is** | Distributed Version Control System (VCS) tool. | Cloud-based hosting service and collaboration platform. |
| **Where it runs** | Locally on your computer (offline-capable). | In the cloud / on web servers (requires internet). |
| **Primary purpose** | Tracks history, records changes, and manages branches. | Hosts repositories, handles Pull Requests, CI/CD, and team reviews. |
| **Interface** | Command Line Interface (CLI) & desktop clients. | Web UI, GitHub Desktop, GitHub CLI (`gh`), and REST/GraphQL API. |
| **Creator** | Linus Torvalds (2005). | Chris Wanstrath, P. J. Hyett, Tom Preston-Werner (2008 / Microsoft). |

> **Key Takeaway:** Git is the engine that records your code history; GitHub is the platform where you share that history with others.

---

## 📁 Repository Structure

```text
.
├── README.md
├── git-local-commands/
│   └── README.md          # Guide for local Git operations & offline workflows
└── github-cloud-commands/
    └── README.md          # Guide for remote GitHub operations, PRs & GitHub CLI
```

---

## 🚀 Quick Setup for Beginners

### Step 1: Install Git
- **Windows**: Download from [git-scm.com](https://git-scm.com/) or run `winget install --id Git.Git -e --source winget`.
- **macOS**: Run `brew install git` or install Xcode Command Line Tools (`xcode-select --install`).
- **Linux (Ubuntu/Debian)**: Run `sudo apt update && sudo apt install git -y`.

### Step 2: Configure Global Identity
Run these commands in your terminal to associate commits with your name and email:

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

### Step 3: Set Default Branch Name to `main`
```bash
git config --global init.defaultBranch main
```

### Step 4: Verify Configuration
```bash
git config --list
```

---

## 🧭 Navigation & Modules

- 📦 **[Local Git Operations Guide](git-local-commands/README.md)**: Setup, staging, committing, history inspection, branching, merging, stashing, and undoing changes.
- ☁️ **[GitHub Cloud Operations Guide](github-cloud-commands/README.md)**: Remotes, cloning, pushing, pulling, PR workflows, and GitHub CLI tools.
