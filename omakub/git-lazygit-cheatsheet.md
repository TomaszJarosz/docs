# Git & Lazygit - Cheatsheet

## Git - Command Line

### Basic Configuration

```bash
# Set user data
git config --global user.name "Your Name"
git config --global user.email "email@example.com"

# Editor
git config --global core.editor "nvim"

# Aliases (useful!)
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"

# View configuration
git config --list
git config --global --edit
```

### Basic Commands

**Initialization and Cloning:**
```bash
git init                          # New repo
git clone url                     # Clone repo
git clone url folder             # Clone to folder
git clone --depth 1 url          # Shallow clone (faster)
```

**Status and Information:**
```bash
git status                        # Repository status
git status -s                     # Short status
git diff                          # Changes (unstaged)
git diff --staged                 # Changes (staged)
git diff HEAD                     # All changes
git diff branch1 branch2          # Differences between branches
git log                           # Commit history
git log --oneline                 # Short history
git log --graph --all             # Graphical history
git show commit_hash              # Show commit
```

**Staging and Commits:**
```bash
git add file.txt                  # Add file
git add .                         # Add all
git add -p                        # Interactive adding (by hunk)
git reset file.txt                # Unstage file
git reset                         # Unstage everything

git commit -m "message"           # Commit
git commit -am "message"          # Add + commit (tracked files only)
git commit --amend                # Amend last commit
git commit --amend --no-edit      # Amend without changing message
```

**Branches:**
```bash
git branch                        # List branches
git branch name                   # New branch
git branch -d name                # Delete branch (safe)
git branch -D name                # Delete branch (force)
git checkout name                 # Switch to branch
git checkout -b name              # Create and switch
git switch name                   # Switch (newer command)
git switch -c name                # Create and switch (newer)
git merge name                    # Merge branch
git rebase main                   # Rebase on main
```

**Remote (Remote Repo):**
```bash
git remote                        # List remote
git remote -v                     # List with URL
git remote add origin url         # Add remote
git remote remove origin          # Remove remote
git remote rename old new         # Rename

git fetch                         # Fetch changes
git fetch origin                  # Fetch from origin
git pull                          # Fetch + merge
git pull --rebase                 # Fetch + rebase
git push                          # Push changes
git push origin branch            # Push to branch
git push -u origin branch         # Push and set upstream
git push --force                  # Force push (CAREFUL!)
git push --force-with-lease       # Safer force push
```

**Undoing Changes:**
```bash
# Unstage (undo git add)
git reset file.txt
git reset HEAD file.txt

# Discard changes in file (working directory)
git checkout -- file.txt
git restore file.txt              # Newer command

# Undo commit (keep changes)
git reset --soft HEAD~1

# Undo commit (discard changes)
git reset --hard HEAD~1

# Undo commit (create new reverting commit)
git revert commit_hash

# Clean working directory
git clean -n                      # Dry run
git clean -f                      # Remove untracked files
git clean -fd                     # Remove untracked files and folders
```

**Stash:**
```bash
git stash                         # Stash changes
git stash save "description"      # Stash with description
git stash list                    # List stash
git stash pop                     # Restore and remove stash
git stash apply                   # Restore (keep stash)
git stash drop                    # Remove stash
git stash clear                   # Clear all stash
git stash show -p                 # Show stash contents
```

**Tags:**
```bash
git tag                           # List tags
git tag v1.0.0                    # Lightweight tag
git tag -a v1.0.0 -m "Release"   # Annotated tag
git tag -d v1.0.0                 # Delete tag locally
git push origin v1.0.0            # Push tag
git push origin --tags            # Push all tags
git push origin :refs/tags/v1.0.0 # Delete tag from remote
```

### Advanced

**Interactive Rebase:**
```bash
git rebase -i HEAD~3              # Edit last 3 commits
# In editor:
# pick = keep commit
# reword = change message
# edit = stop and edit
# squash = combine with previous
# fixup = squash without message
# drop = delete commit
```

**Cherry-pick:**
```bash
git cherry-pick commit_hash       # Apply commit from another branch
git cherry-pick A B C             # Multiple commits
git cherry-pick --abort           # Cancel
```

**Blame and History:**
```bash
git blame file.txt                # Who changed each line
git log -p file.txt               # File change history
git log --follow file.txt         # History with renames
git log --grep="pattern"          # Search in commits
git log --author="name"           # Author's commits
git log --since="2 weeks ago"     # Last 2 weeks
```

**Bisect (Find Bug):**
```bash
git bisect start                  # Start
git bisect bad                    # Mark as bad
git bisect good commit_hash       # Mark good commit
# Git automatically tests commits
git bisect good/bad               # Mark subsequent ones
git bisect reset                  # Finish
```

**Submodules:**
```bash
git submodule add url path        # Add submodule
git submodule init                # Initialize
git submodule update              # Update
git clone --recursive url         # Clone with submodules
```

**Worktree (Multiple Working Directories):**
```bash
git worktree add ../feature feature-branch
git worktree list
git worktree remove ../feature
```

## Lazygit - Terminal UI for Git

**Launch:**
```bash
lazygit
# or alias in Omakub:
lg
```

### Main Panels

Lazygit has 5 main panels:
1. **Status** - Repository status
2. **Files** - Files (changes)
3. **Branches** - Branches
4. **Commits** - Commit history
5. **Stash** - Stashed changes

### Navigation in Lazygit

| Shortcut | Action |
|-------|-------|
| `1-5` | Switch between panels (Status, Files, Branches, Commits, Stash) |
| `h/l` or `←/→` | Switch between panels |
| `j/k` or `↑/↓` | Navigate in panel |
| `[/]` | Previous/next panel |
| `</>` | Scroll in main panel |
| `Ctrl+u/d` | Scroll up/down (half page) |
| `q` | Quit / Go back |
| `Esc` | Cancel / Go back |
| `?` | Help (see all shortcuts!) |

### Files Panel

| Shortcut | Action |
|-------|-------|
| `Space` | Stage/unstage file or hunk |
| `a` | Stage/unstage all |
| `d` | Discard changes |
| `e` | Edit file |
| `o` | Open file |
| `i` | Add to .gitignore |
| `r` | Refresh files |
| `s` | Stash all changes |
| `S` | Stash options (menu) |
| `M` | Commit (open message editor) |
| `c` | Commit (inline message) |
| `A` | Amend last commit |
| `Enter` | Stage individual lines (stage hunks) |

**In hunk view (Enter on file):**
| Shortcut | Action |
|-------|-------|
| `Space` | Stage/unstage hunk |
| `a` | Stage/unstage file |
| `e` | Edit hunk |
| `Esc` | Return to file list |

### Commits Panel

| Shortcut | Action |
|-------|-------|
| `Space` | Checkout commit |
| `c` | Checkout commit (detached) |
| `r` | Reword commit (change message) |
| `R` | Reword with editor |
| `g` | Reset to commit (mixed) |
| `s` | Squash down (combine with previous) |
| `f` | Fixup commit |
| `d` | Delete commit (drop) |
| `e` | Edit commit |
| `p` | Pick commit (cherry-pick) |
| `C` | Copy commit (sha) |
| `A` | Amend commit |
| `Enter` | View files in commit |
| `v` | Paste (commits) |
| `t` | Revert commit |
| `T` | Tag commit |

**Interactive rebase:**
| Shortcut | Action |
|-------|-------|
| `i` | Start interactive rebase |
| `e` | Edit (in rebase mode) |
| `m` | Move commit down |
| `M` | Move commit up |

### Branches Panel

| Shortcut | Action |
|-------|-------|
| `Space` | Checkout branch |
| `n` | New branch |
| `o` | Create pull request |
| `c` | Checkout by name |
| `r` | Rebase branch |
| `M` | Merge to current branch |
| `i` | Show git-flow options |
| `d` | Delete branch |
| `D` | Force delete |
| `F` | Fast-forward |
| `g` | Reset (from options menu) |
| `R` | Rename branch |
| `Enter` | View commits |
| `w` | View merge/rebase options |

### Stash Panel

| Shortcut | Action |
|-------|-------|
| `Space` | Apply stash |
| `g` | Pop stash |
| `d` | Drop stash |
| `n` | New stash |
| `r` | Rename stash |

### Remote Operations (Push/Pull)

| Shortcut | Action |
|-------|-------|
| `p` | Pull |
| `P` | Push |
| `Shift+P` | Push force |
| `f` | Fetch |
| `F` | Force fetch |

### General

| Shortcut | Action |
|-------|-------|
| `x` | Open options menu |
| `!` | Open command log |
| `@` | Open command log menu |
| `z` | Undo |
| `Ctrl+z` | Redo |
| `:` | Execute custom command |
| `+` | Next screen mode |
| `_` | Previous screen mode |
| `Ctrl+r` | Recently used repo (switch) |
| `Ctrl+e` | Open lazygit config |

### Search and Filtering

| Shortcut | Action |
|-------|-------|
| `/` | Start search (filter) |
| `Ctrl+s` | View filter-by-path options |
| `Ctrl+/` | Regex toggle |

## Workflow Tips

### 1. Basic Workflow with Lazygit

```bash
# Launch lazygit
lazygit

# In lazygit:
1. Files panel (2)
2. Space - stage files
3. c - commit with message
4. P - push
```

### 2. Interactive Staging (Hunks)

In lazygit:
1. Files panel
2. `Enter` on file - view hunks
3. `Space` - stage selected hunks
4. `Esc` - go back
5. `c` - commit

### 3. Amending Commits

**Add changes to last commit:**
```bash
# In lazygit:
1. Change file
2. Files panel
3. Space - stage
4. A - amend last commit
```

**Change message of last commit:**
```bash
# In lazygit:
1. Commits panel
2. r on last commit
```

### 4. Interactive Rebase

```bash
# In lazygit:
1. Commits panel
2. i - start interactive rebase
3. Use s/f/d for squash/fixup/drop
4. m/M - move commits
5. Ctrl+o - continue rebase
```

### 5. Branch Workflow

```bash
# New feature branch:
1. Branches panel
2. n - new branch
3. Enter name

# Merge to main:
1. Checkout main (Space on main)
2. Branches panel
3. M on feature branch - merge
```

### 6. Stash Workflow

```bash
# Stash changes:
1. Files panel
2. s - stash all

# Restore:
1. Stash panel
2. Space - apply (or g - pop)
```

### 7. Cherry-pick

```bash
1. Commits panel (other branch)
2. p on commit - cherry-pick
3. Switch to target branch
4. v - paste (apply cherry-pick)
```

### 8. Resolving Conflicts

```bash
# After merge/rebase with conflicts:
1. Files panel - files with conflicts marked
2. e - edit file (opens in nvim)
3. Resolve conflicts
4. :wq - save and exit
5. Space - stage resolved file
6. c - commit (or continue rebase)
```

## Git Best Practices

### Commit Messages

**Format:**
```
type: short description (max 50 characters)

Longer description if needed (wrap at 72 chars)
- Point 1
- Point 2

Fixes #123
```

**Types:**
- `feat:` - new feature
- `fix:` - bug fix
- `docs:` - documentation
- `style:` - formatting (doesn't affect code)
- `refactor:` - refactoring
- `test:` - tests
- `chore:` - maintenance

### Branch Naming

```bash
feature/feature-name
bugfix/bug-name
hotfix/urgent-fix
release/v1.2.3
```

### Workflow Strategies

**1. Feature Branch Workflow:**
```bash
git checkout -b feature/new-feature
# Work...
git add .
git commit -m "feat: add new feature"
git push -u origin feature/new-feature
# Pull request/merge to main
```

**2. Git Flow:**
```bash
# Main branches: main, develop
# Supporting: feature/*, release/*, hotfix/*

git checkout -b develop
git checkout -b feature/feature-name
# Work...
git checkout develop
git merge feature/feature-name
```

**3. Rebase Before Merge:**
```bash
git checkout feature
git rebase main           # Update from main
git push --force-with-lease
# Then merge to main
```

### Useful .gitconfig Snippets

```ini
[core]
    editor = nvim
    autocrlf = input
    pager = delta           # Better diff (if installed)

[alias]
    st = status -sb
    co = checkout
    br = branch
    ci = commit
    unstage = reset HEAD --
    undo = reset --soft HEAD^
    lg = log --graph --oneline --all --decorate
    last = log -1 HEAD
    amend = commit --amend --no-edit

[pull]
    rebase = true           # Default to pull --rebase

[push]
    default = current       # Push to branch with same name
    followTags = true       # Automatically push tags

[fetch]
    prune = true            # Remove old remote branches

[diff]
    colorMoved = zebra      # Better display of moved lines

[merge]
    conflictstyle = diff3   # Better conflict display

[rerere]
    enabled = true          # Remember how you resolved conflicts
```

## .gitignore Patterns

```gitignore
# OS
.DS_Store
Thumbs.db

# Editors
.vscode/
.idea/
*.swp
*.swo
*~

# Languages
## Node
node_modules/
npm-debug.log
yarn-error.log

## Python
__pycache__/
*.py[cod]
*.pyo
.env
venv/
.pytest_cache/

## Ruby
*.gem
.bundle/

## Rust
target/

# Build outputs
dist/
build/
*.log

# Secrets
.env
.env.local
credentials.json
*.key
*.pem
```

## Useful Git Aliases (Bash)

Add to `~/.bashrc`:
```bash
alias g='git'
alias gs='git status'
alias ga='git add'
alias gc='git commit'
alias gp='git push'
alias gl='git pull'
alias gd='git diff'
alias gco='git checkout'
alias gb='git branch'
alias glog='git log --oneline --graph --decorate'
alias lg='lazygit'

# Functions
gac() {
    git add .
    git commit -m "$1"
}

gacp() {
    git add .
    git commit -m "$1"
    git push
}

# Usage:
# gac "fix: update readme"
# gacp "feat: add new feature"
```

## Resources

- **Git Docs:** https://git-scm.com/doc
- **Lazygit:** https://github.com/jesseduffield/lazygit
- **Interactive Tutorial:** https://learngitbranching.js.org/
- **Git Cheatsheet:** https://education.github.com/git-cheat-sheet-education.pdf
- `man git` - Documentation
- `git help <command>` - Help for command

## Quick Start

**Git:**
```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin url
git push -u origin main
```

**Lazygit:**
```bash
lazygit
# 2 - Files
# Space - Stage
# c - Commit
# P - Push
```

**Remember:**
- Commit often, in small chunks
- Use good commit messages
- Rebase before merge (clean history)
- Never force push to shared branch
- Lazygit = fast visual workflow
