# 🚀 GitHub Setup Guide - Command Line

> **Quick Start**: New to GitHub? Jump to [🏃‍♂️ Quick Setup](#-quick-setup) for the fastest way to get started!

## 📋 Table of Contents

- [🏃‍♂️ Quick Setup](#️-quick-setup)
- [⚙️ Detailed Setup](#️-detailed-setup)
  - [📦 Install Git](#-install-git)
  - [👤 Configure Your Identity](#-configure-your-identity)
  - [🔐 Setup Authentication](#-setup-authentication)
- [📁 Working with Repositories](#-working-with-repositories)
  - [🆕 Create New Repository](#-create-new-repository)
  - [📥 Clone Existing Repository](#-clone-existing-repository)
- [💼 Daily Commands](#-daily-commands)
- [🛠️ Advanced Tools](#️-advanced-tools)
- [🆘 Troubleshooting](#-troubleshooting)
- [📚 Quick Reference](#-quick-reference)

---

## 🏃‍♂️ Quick Setup

**Already have Git installed? Skip to step 3!**

1. **Install Git** (if needed):
   ```bash
   sudo apt update && sudo apt install git
   ```

2. **Configure your identity**:
   ```bash
   git config --global user.name "Your Name"
   git config --global user.email "your.email@example.com"
   ```

3. **Setup SSH key** (recommended):
   ```bash
   ssh-keygen -t ed25519 -C "your.email@example.com"
   cat ~/.ssh/id_ed25519.pub
   ```
   Copy the output and add it to GitHub: [Settings → SSH Keys](https://github.com/settings/keys)

4. **Test connection**:
   ```bash
   ssh -T git@github.com
   ```

5. **You're ready!** 🎉

---

## ⚙️ Detailed Setup

### 📦 Install Git

<details>
<summary><strong>🐧 Linux Installation</strong></summary>

**Ubuntu/Debian:**
```bash
sudo apt update
sudo apt install git
```

**CentOS/RHEL:**
```bash
sudo yum install git
```

**Fedora:**
```bash
sudo dnf install git
```

**Verify installation:**
```bash
git --version
```
</details>

---

### 👤 Configure Your Identity

```bash
# Set your name and email (required)
git config --global user.name "Your Full Name"
git config --global user.email "your.email@example.com"

# Set default branch name to 'main'
git config --global init.defaultBranch main

# Check your settings
git config --list
```

---

### 🔐 Setup Authentication

<details>
<summary><strong>🔑 SSH Keys (Recommended)</strong></summary>

**Step 1: Generate SSH key**
```bash
ssh-keygen -t ed25519 -C "your.email@example.com"
# Press Enter for default location, set passphrase if desired
```

**Step 2: Add key to SSH agent**
```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

**Step 3: Copy public key**
```bash
cat ~/.ssh/id_ed25519.pub
# Copy the entire output
```

**Step 4: Add to GitHub**
1. Go to [GitHub SSH Settings](https://github.com/settings/keys)
2. Click "New SSH key"
3. Paste your key and give it a title
4. Click "Add SSH key"

**Step 5: Test connection**
```bash
ssh -T git@github.com
```
</details>

<details>
<summary><strong>🔗 HTTPS with Personal Access Token</strong></summary>

**Step 1: Create token**
1. Go to [GitHub Tokens](https://github.com/settings/tokens)
2. Click "Generate new token (classic)"
3. Select scopes: `repo`, `workflow`
4. Copy the token immediately!

**Step 2: Configure Git**
```bash
git config --global credential.helper store
```

**When prompted for password, use your token instead**
</details>

---

## 📁 Working with Repositories

### 🆕 Create New Repository

**Method 1: Start locally**
```bash
# Create project folder
mkdir my-awesome-project
cd my-awesome-project

# Initialize Git
git init

# Create README
echo "# My Awesome Project" > README.md

# First commit
git add README.md
git commit -m "🎉 Initial commit"

# Connect to GitHub (create repo on GitHub first!)
git remote add origin git@github.com:yourusername/my-awesome-project.git
git push -u origin main
```

**Method 2: Start on GitHub**
1. Create repository on GitHub
2. Clone it locally:
```bash
git clone git@github.com:yourusername/repository-name.git
cd repository-name
```

### 📥 Clone Existing Repository

```bash
# SSH (recommended)
git clone git@github.com:username/repository-name.git

# HTTPS
git clone https://github.com/username/repository-name.git
```

---

## 💼 Daily Commands

### 📊 Check Status
```bash
git status                 # See what's changed
git log --oneline         # View commit history
git diff                  # See changes in detail
```

### 📝 Making Changes
```bash
# Add files to staging
git add filename.txt      # Add specific file
git add .                # Add all changes

# Commit changes
git commit -m "✨ Add awesome feature"

# Push to GitHub
git push
```

### 🔄 Sync with Remote
```bash
git pull                  # Get latest changes
git fetch                # Get updates without merging
```

### 🌿 Working with Branches
```bash
# Create and switch to new branch
git checkout -b feature/awesome-feature

# Switch between branches
git checkout main
git checkout feature/awesome-feature

# Merge branch (switch to main first)
git checkout main
git merge feature/awesome-feature

# Delete branch after merging
git branch -d feature/awesome-feature
```

---

## 🛠️ Advanced Tools

### 🔧 GitHub CLI

<details>
<summary><strong>Install and use GitHub CLI for power users</strong></summary>

**Install:**
```bash
curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null
sudo apt update && sudo apt install gh
```

**Authenticate:**
```bash
gh auth login
```

**Useful commands:**
```bash
gh repo create my-new-repo --public --clone
gh issue list
gh pr create --title "Feature" --body "Description"
gh pr list
```
</details>

### ⚡ Useful Git Configurations

```bash
# Set your preferred editor
git config --global core.editor "code --wait"    # VS Code
git config --global core.editor "nano"           # Nano

# Enable colored output
git config --global color.ui auto

# Better push behavior
git config --global push.default simple
```

---

## 🆘 Troubleshooting

### 😱 I Messed Up! Common Fixes

<details>
<summary><strong>🔄 Undo changes</strong></summary>

```bash
# Discard all local changes (be careful!)
git reset --hard HEAD
git clean -fd

# Undo last commit but keep changes
git reset --soft HEAD~1

# Change last commit message
git commit --amend -m "Better commit message"
```
</details>

<details>
<summary><strong>🔀 Branch issues</strong></summary>

```bash
# Switch branches with uncommitted changes
git stash                    # Save changes temporarily
git checkout other-branch
git stash pop               # Restore changes

# Delete branch that won't delete
git branch -D branch-name   # Force delete
```
</details>

<details>
<summary><strong>🌐 Remote issues</strong></summary>

```bash
# Force push (use carefully!)
git push --force-with-lease

# Change remote URL
git remote set-url origin git@github.com:username/repo.git

# Remove remote
git remote remove origin
```
</details>

---

## 📚 Quick Reference

### 🏃‍♂️ Speed Commands
```bash
# Super quick workflow
git add . && git commit -m "Quick update" && git push

# Check everything at once
git status && git log --oneline -5
```

### 📋 Essential Commands Cheatsheet

| Command | What it does |
|---------|-------------|
| `git status` | Check what's changed |
| `git add .` | Stage all changes |
| `git commit -m "message"` | Save changes with message |
| `git push` | Upload to GitHub |
| `git pull` | Download latest changes |
| `git checkout -b name` | Create new branch |
| `git checkout main` | Switch to main branch |
| `git log --oneline` | View commit history |

### 🔒 Security Checklist

- ✅ Use SSH keys instead of passwords
- ✅ Enable 2FA on GitHub account  
- ✅ Never commit secrets (use `.gitignore`)
- ✅ Regularly update access tokens
- ✅ Review repository permissions

---

## 🎯 What's Next?

1. **Practice**: Try creating a test repository
2. **Learn branching**: Master the branch workflow
3. **Explore GitHub**: Issues, Pull Requests, Actions
4. **Join projects**: Contribute to open source
5. **Advanced Git**: Rebase, cherry-pick, hooks

---

**💡 Pro Tip**: Bookmark this guide and refer back to the [Quick Reference](#-quick-reference) section for daily commands!

**🆘 Need help?** Check the [Troubleshooting](#-troubleshooting) section or ask on [GitHub Community](https://github.community/).
