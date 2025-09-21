# GitHub Setup Guide - Command Line

## Prerequisites
- Git installed on your system
- GitHub account created
- Terminal/Command prompt access

## 1. Install Git (if not already installed)

### Linux (Ubuntu/Debian)
```bash
sudo apt update
sudo apt install git
```

### Linux (CentOS/RHEL/Fedora)
```bash
# CentOS/RHEL
sudo yum install git
# or Fedora
sudo dnf install git
```

### Verify Installation
```bash
git --version
```

## 2. Configure Git with Your Information

### Set Global Username and Email
```bash
git config --global user.name "Your Full Name"
git config --global user.email "your.email@example.com"
```

### Set Default Branch Name (optional but recommended)
```bash
git config --global init.defaultBranch main
```

### Verify Configuration
```bash
git config --list
```

## 3. SSH Key Setup (Recommended for Security)

### Generate SSH Key
```bash
ssh-keygen -t ed25519 -C "your.email@example.com"
```

### Start SSH Agent and Add Key
```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

### Copy SSH Key to Clipboard
```bash
# Linux
cat ~/.ssh/id_ed25519.pub | xclip -selection clipboard
# or if xclip not available
cat ~/.ssh/id_ed25519.pub
```

### Add SSH Key to GitHub
1. Go to GitHub.com → Settings → SSH and GPG keys
2. Click "New SSH key"
3. Paste your key and give it a title
4. Click "Add SSH key"

### Test SSH Connection
```bash
ssh -T git@github.com
```

## 4. Alternative: HTTPS with Personal Access Token

### Generate Personal Access Token
1. Go to GitHub.com → Settings → Developer settings → Personal access tokens
2. Click "Generate new token"
3. Select scopes (repo, workflow, etc.)
4. Copy the token (save it securely!)

### Configure Git to Use Token
```bash
git config --global credential.helper store
```

## 5. Create and Initialize a Repository

### Create New Repository on Local Machine
```bash
mkdir my-project
cd my-project
git init
```

### Create Initial Files
```bash
echo "# My Project" > README.md
git add README.md
git commit -m "Initial commit"
```

### Connect to GitHub Repository
```bash
# Create repository on GitHub first, then:
git remote add origin git@github.com:yourusername/your-repo-name.git
# or for HTTPS:
git remote add origin https://github.com/yourusername/your-repo-name.git
```

### Push to GitHub
```bash
git branch -M main
git push -u origin main
```

## 6. Clone Existing Repository

### Clone with SSH
```bash
git clone git@github.com:username/repository-name.git
```

### Clone with HTTPS
```bash
git clone https://github.com/username/repository-name.git
```

## 7. Basic Git Commands for Daily Use

### Check Status
```bash
git status
```

### Add Files to Staging
```bash
git add filename.txt
git add .  # Add all files
```

### Commit Changes
```bash
git commit -m "Your commit message"
```

### Push Changes
```bash
git push
```

### Pull Latest Changes
```bash
git pull
```

### Create and Switch Branch
```bash
git checkout -b feature-branch-name
```

### Switch Between Branches
```bash
git checkout main
git checkout feature-branch-name
```

### Merge Branch
```bash
git checkout main
git merge feature-branch-name
```

### View Commit History
```bash
git log
git log --oneline  # Compact view
```

## 8. GitHub CLI (Optional but Powerful)

### Install GitHub CLI
```bash
# Linux
curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null
sudo apt update
sudo apt install gh
```

### Authenticate with GitHub CLI
```bash
gh auth login
```

### Create Repository with CLI
```bash
gh repo create my-new-repo --public --clone
```

### View Issues and PRs
```bash
gh issue list
gh pr list
```

## 9. Useful Git Configurations

### Set Default Editor
```bash
git config --global core.editor "code --wait"  # VS Code
git config --global core.editor "nano"         # Nano
git config --global core.editor "vim"          # Vim
```

### Enable Colored Output
```bash
git config --global color.ui auto
```

### Set Push Default
```bash
git config --global push.default simple
```

## 10. Common Troubleshooting

### Reset Local Changes
```bash
git reset --hard HEAD  # Discard all local changes
git clean -fd          # Remove untracked files
```

### Undo Last Commit (keep changes)
```bash
git reset --soft HEAD~1
```

### Change Last Commit Message
```bash
git commit --amend -m "New commit message"
```

### Force Push (use carefully)
```bash
git push --force-with-lease
```

## Security Tips

1. **Never commit sensitive information** (passwords, API keys, etc.)
2. **Use .gitignore** to exclude files you don't want to track
3. **Use SSH keys** instead of passwords when possible
4. **Enable two-factor authentication** on your GitHub account
5. **Regularly update your access tokens**

## Quick Reference Card

```bash
# Setup
git config --global user.name "Name"
git config --global user.email "email@example.com"

# Basic workflow
git init
git add .
git commit -m "message"
git remote add origin <url>
git push -u origin main

# Daily use
git status
git add filename
git commit -m "message"
git push
git pull
```

---

**Note**: Replace `yourusername`, `your-repo-name`, `Your Full Name`, and `your.email@example.com` with your actual GitHub username, repository name, full name, and email address.
