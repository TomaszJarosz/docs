# Git Console - Developer Cheatsheet

Practical guide for Git console for efficient work without GUI.

## Philosophy of Working with Git in Console

**Why console?**
- Speed - no clicking
- Automation - scripts and aliases
- Full control - access to all options
- Universality - works everywhere (SSH, CI/CD)

## Quick Configuration

### Basic Configuration

```bash
# User data
git config --global user.name "Your Name"
git config --global user.email "email@example.com"

# Editor
git config --global core.editor "nvim"

# Colors
git config --global color.ui auto

# Default branch
git config --global init.defaultBranch main

# Pull with rebase instead of merge
git config --global pull.rebase true

# Push only current branch
git config --global push.default current

# Automatic removal of dead remote branches
git config --global fetch.prune true

# Better conflict display
git config --global merge.conflictstyle diff3

# Remember conflict resolutions
git config --global rerere.enabled true
```

### Useful Aliases

Add to `~/.gitconfig`:

```ini
[alias]
    # Status
    s = status -sb
    st = status

    # Log
    l = log --oneline --graph --decorate
    lg = log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit
    ll = log --oneline --graph --all --decorate
    today = log --since='00:00:00' --all --no-merges --oneline --author=<your-email>

    # Diff
    d = diff
    ds = diff --staged
    dc = diff --cached

    # Commit
    c = commit
    cm = commit -m
    ca = commit --amend
    can = commit --amend --no-edit

    # Branch
    b = branch
    ba = branch -a
    bd = branch -d
    bD = branch -D

    # Checkout
    co = checkout
    cob = checkout -b

    # Switch (newer commands)
    sw = switch
    swc = switch -c

    # Remote
    f = fetch
    fo = fetch origin
    p = push
    pl = pull

    # Stash
    ss = stash save
    sp = stash pop
    sl = stash list

    # Reset
    unstage = reset HEAD --
    undo = reset --soft HEAD^

    # Misc
    last = log -1 HEAD
    aliases = config --get-regexp alias
    contributors = shortlog -sn --all --no-merges
```

Usage:
```bash
git s          # git status -sb
git lg         # beautiful log
git cm "msg"   # commit with message
```

## Daily Workflow

### Starting Work

```bash
# Check status
git status

# Update from remote
git pull --rebase

# Or safer (fetch + merge/rebase)
git fetch
git rebase origin/main
```

### Working on Changes

```bash
# See what changed
git status
git diff                  # unstaged changes
git diff --staged         # staged changes

# Add changes
git add file.txt          # specific file
git add .                 # everything in current directory
git add -A                # everything in repo
git add -p                # interactively (piece by piece)

# Undo git add
git reset HEAD file.txt   # unstage file
git reset                 # unstage everything

# Discard local changes
git checkout -- file.txt  # old syntax
git restore file.txt      # new syntax
```

### Commit

```bash
# Basic commit
git commit -m "feat: add user authentication"

# Multi-line commit message
git commit -m "feat: add user authentication" -m "- Add login endpoint
- Add JWT token generation
- Add password hashing"

# Commit all tracked files
git commit -am "fix: resolve validation bug"

# Fix last commit (message)
git commit --amend -m "new message"

# Fix last commit (add files)
git add forgotten-file.txt
git commit --amend --no-edit

# Commit with date
git commit --date="2024-01-15 10:00:00" -m "msg"
```

### Commit Message Convention

Format: `<type>: <subject>`

**Types:**
- `feat` - new feature
- `fix` - bug fix
- `docs` - documentation
- `style` - formatting (no logic changes)
- `refactor` - refactoring
- `perf` - performance optimization
- `test` - tests
- `chore` - maintenance, dependencies
- `ci` - CI/CD
- `build` - build system

**Examples:**
```bash
git commit -m "feat: add password reset functionality"
git commit -m "fix: resolve null pointer in user service"
git commit -m "docs: update API documentation"
git commit -m "refactor: simplify authentication logic"
```

## Branches

### Branch Management

```bash
# List branches
git branch                # local
git branch -a             # all (remote + local)
git branch -v             # with last commit
git branch -vv            # with tracking info

# New branch
git branch feature/login
git checkout -b feature/login         # create and switch
git switch -c feature/login           # newer syntax

# Switching
git checkout main
git switch main

# Rename
git branch -m old-name new-name
git branch -m new-name              # rename current branch

# Delete
git branch -d feature/done            # safe (checks if merged)
git branch -D feature/abandoned       # force

# Delete remote branch
git push origin --delete feature/old
```

### Branch Workflow

```bash
# Feature branch workflow
git checkout main
git pull
git checkout -b feature/new-feature

# ... work ...
git add .
git commit -m "feat: implement new feature"

# Update from main before merge
git checkout main
git pull
git checkout feature/new-feature
git rebase main           # or: git merge main

# Send to remote
git push -u origin feature/new-feature

# After merge in GitHub/GitLab
git checkout main
git pull
git branch -d feature/new-feature
```

## Remote Operations

### Basics

```bash
# List remotes
git remote -v

# Add remote
git remote add origin https://github.com/user/repo.git

# Change URL
git remote set-url origin git@github.com:user/repo.git

# Remove remote
git remote remove origin

# Rename remote
git remote rename origin upstream
```

### Fetch, Pull, Push

```bash
# Fetch - download changes (no merge)
git fetch origin
git fetch --all
git fetch --prune         # remove dead remote branches

# Pull - fetch + merge/rebase
git pull
git pull --rebase         # recommended
git pull origin main

# Push
git push
git push origin main
git push -u origin feature/new      # set upstream
git push --force-with-lease         # safer force push
git push --all                      # all branches

# Push tags
git push --tags
```

### Working with Fork

```bash
# Add upstream (original project)
git remote add upstream https://github.com/original/repo.git

# Sync with upstream
git fetch upstream
git checkout main
git merge upstream/main
# or:
git rebase upstream/main

# Push to your fork
git push origin main
```

## History and Log

### Browsing History

```bash
# Basic log
git log
git log --oneline
git log --graph --all
git log -10                   # last 10 commits
git log --since="2 weeks ago"
git log --after="2024-01-01"
git log --author="John Doe"
git log --grep="fix"          # search in messages

# Log for file
git log file.txt
git log -p file.txt           # with diff
git log --follow file.txt     # track name changes

# Statistics
git log --stat
git log --shortstat
git shortlog -sn              # commit count per author

# Beautiful format
git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset'
```

### Show, Diff, Blame

```bash
# Show commit
git show commit-hash
git show HEAD
git show HEAD~2               # 2 commits back

# Diff
git diff                      # working vs staged
git diff --staged             # staged vs last commit
git diff HEAD                 # working vs last commit
git diff branch1 branch2
git diff commit1 commit2
git diff main...feature       # from common ancestor

# Blame - who changed line
git blame file.txt
git blame -L 10,20 file.txt   # only lines 10-20
git blame -w file.txt         # ignore whitespace
git blame -C file.txt         # detect code copying
```

## Undoing Changes

### Reset vs Revert

```bash
# Reset - undo commits (changes history!)
git reset --soft HEAD~1       # undo commit, keep changes (staged)
git reset --mixed HEAD~1      # undo commit, changes unstaged (default)
git reset --hard HEAD~1       # undo commit, DELETE changes

# Reset to specific commit
git reset --hard abc123

# Revert - creates new undoing commit (safe!)
git revert HEAD
git revert commit-hash
git revert HEAD~3
```

### Practical Undoing

```bash
# I want to undo last commit (not pushed)
git reset --soft HEAD~1

# I want to undo last commit and changes
git reset --hard HEAD~1

# I want to undo commit that was already pushed
git revert HEAD

# I want to remove uncommitted changes
git restore file.txt
git restore .

# I want to remove all local changes
git reset --hard HEAD
git clean -fd                 # remove untracked files

# I committed to wrong branch
git reset --soft HEAD~1
git stash
git checkout correct-branch
git stash pop
git commit
```

## Stash

### Basics

```bash
# Stash changes
git stash
git stash save "work in progress"
git stash push -m "WIP: feature X"

# List stash
git stash list

# Restore
git stash pop                 # apply + drop
git stash apply               # apply (keep in stash)
git stash apply stash@{2}     # specific stash

# Remove
git stash drop stash@{0}
git stash clear               # remove all

# See what's in stash
git stash show
git stash show -p             # with diff
```

### Advanced Stash

```bash
# Stash only unstaged
git stash --keep-index

# Stash with untracked files
git stash -u

# Stash specific files
git stash push file1.txt file2.txt

# Create branch from stash
git stash branch feature/new-branch
```

## Rebase - Rewriting History

### Basic Rebase

```bash
# Rebase onto another branch
git checkout feature
git rebase main

# Or shorter
git rebase main feature

# Continue after resolving conflicts
git add resolved-file.txt
git rebase --continue

# Skip commit
git rebase --skip

# Cancel rebase
git rebase --abort
```

### Interactive Rebase

```bash
# Edit last N commits
git rebase -i HEAD~3

# In editor:
pick abc123 First commit
pick def456 Second commit
pick ghi789 Third commit

# Possible actions:
# pick   = use commit
# reword = use commit, but change message
# edit   = stop for editing
# squash = merge with previous (keep message)
# fixup  = merge with previous (discard message)
# drop   = remove commit
```

### Practical Examples

```bash
# Merge last 3 commits into one
git rebase -i HEAD~3
# Change: pick, squash, squash

# Change message of last commit
git commit --amend -m "new message"

# Change message of older commit
git rebase -i HEAD~5
# Change pick to reword for selected commit

# Remove commit from history
git rebase -i HEAD~10
# Change pick to drop (or delete line)

# Change commit order
git rebase -i HEAD~5
# Simply change line order

# Split commit into several
git rebase -i HEAD~3
# Change pick to edit
# After stopping:
git reset HEAD^
git add file1.txt
git commit -m "first part"
git add file2.txt
git commit -m "second part"
git rebase --continue
```

## Cherry-pick

```bash
# Apply specific commit from another branch
git cherry-pick commit-hash

# Multiple commits
git cherry-pick abc123 def456 ghi789

# Cherry-pick without commit (only add changes)
git cherry-pick -n commit-hash

# Continue after resolving conflicts
git cherry-pick --continue

# Cancel
git cherry-pick --abort
```

## Tags

```bash
# List tags
git tag
git tag -l "v1.*"

# Create tag
git tag v1.0.0                              # lightweight
git tag -a v1.0.0 -m "Release version 1.0"  # annotated

# Tag for old commit
git tag -a v0.9.0 commit-hash -m "message"

# Show tag
git show v1.0.0

# Push tags
git push origin v1.0.0
git push origin --tags                      # all

# Delete tag
git tag -d v1.0.0                          # locally
git push origin --delete v1.0.0            # remote
```

## Advanced Operations

### Bisect - Find Bug

```bash
# Start bisect
git bisect start
git bisect bad                    # current commit is bad
git bisect good v1.0.0            # this commit was good

# Git automatically checkouts middle commit
# Test application and mark:
git bisect good                   # works
# or
git bisect bad                    # doesn't work

# Git checkouts next commit to test
# Repeat until you find bad commit

# Finish
git bisect reset
```

### Reflog - HEAD History

```bash
# Show HEAD history (all changes)
git reflog

# Restore deleted commit
git reflog
# Find hash of deleted commit
git checkout commit-hash
git checkout -b recovery-branch

# Undo bad reset
git reflog
git reset --hard HEAD@{2}
```

### Worktree - Multiple Directories

```bash
# Add additional working directory
git worktree add ../feature-branch feature/new-feature

# List worktrees
git worktree list

# Remove worktree
git worktree remove ../feature-branch

# Usage:
cd ../feature-branch
# You work in separate directory, but same repo!
```

### Submodules

```bash
# Add submodule
git submodule add https://github.com/user/repo.git libs/repo

# Clone repo with submodules
git clone --recursive https://github.com/user/main-repo.git

# Update submodules
git submodule update --init --recursive
git submodule update --remote

# Remove submodule
git submodule deinit libs/repo
git rm libs/repo
```

## Practical Workflows

### Feature Branch Workflow

```bash
# 1. Start new feature
git checkout main
git pull
git checkout -b feature/user-auth

# 2. Work
# ... code ...
git add .
git commit -m "feat: implement user authentication"

# 3. Push to remote
git push -u origin feature/user-auth

# 4. Before merge: update from main
git fetch origin
git rebase origin/main

# 5. Resolve conflicts if any
git add resolved-files
git rebase --continue

# 6. Force push (safely)
git push --force-with-lease

# 7. After merge through PR/MR
git checkout main
git pull
git branch -d feature/user-auth
git remote prune origin
```

### Hotfix Workflow

```bash
# 1. Urgent fix
git checkout main
git pull
git checkout -b hotfix/critical-bug

# 2. Fix
# ... fix ...
git add .
git commit -m "fix: resolve critical security issue"

# 3. Push and merge ASAP
git push -u origin hotfix/critical-bug

# 4. After merge
git checkout main
git pull
git branch -d hotfix/critical-bug
```

### Release Workflow

```bash
# 1. Create release branch
git checkout -b release/v1.2.0 develop

# 2. Prepare release
# ... tests, documentation ...
git commit -am "chore: prepare v1.2.0 release"

# 3. Merge to main and tag
git checkout main
git merge --no-ff release/v1.2.0
git tag -a v1.2.0 -m "Version 1.2.0"

# 4. Merge back to develop
git checkout develop
git merge --no-ff release/v1.2.0

# 5. Delete release branch
git branch -d release/v1.2.0

# 6. Push everything
git push origin main develop --tags
```

## Resolving Conflicts

### Process

```bash
# 1. Conflict during merge/rebase
git status                    # see conflicted files

# 2. Open file - you'll see markers:
<<<<<<< HEAD
Your version
=======
Their version
>>>>>>> branch-name

# 3. Edit manually or use tools
git mergetool

# 4. After resolving
git add resolved-file.txt

# 5. Continue operation
git rebase --continue         # for rebase
git merge --continue          # for merge
git commit                    # for merge (if needed)

# Or cancel
git rebase --abort
git merge --abort
```

### Merge Strategies

```bash
# Merge with conflicts - choose strategy
git merge --strategy-option theirs feature
git merge --strategy-option ours feature

# Accept everything from their side
git checkout --theirs file.txt

# Accept everything from our side
git checkout --ours file.txt
```

## Bash Aliases for Git

Add to `~/.bashrc`:

```bash
# Git shortcuts
alias g='git'
alias gs='git status -sb'
alias ga='git add'
alias gaa='git add -A'
alias gc='git commit'
alias gcm='git commit -m'
alias gca='git commit --amend'
alias gcan='git commit --amend --no-edit'
alias gp='git push'
alias gpu='git push -u origin HEAD'
alias gpl='git pull --rebase'
alias gf='git fetch'
alias gd='git diff'
alias gds='git diff --staged'
alias gl='git log --oneline --graph --decorate'
alias gll='git log --oneline --graph --all --decorate'
alias gco='git checkout'
alias gcob='git checkout -b'
alias gb='git branch'
alias gba='git branch -a'
alias gbd='git branch -d'
alias gst='git stash'
alias gstp='git stash pop'
alias gr='git rebase'
alias gri='git rebase -i'
alias grc='git rebase --continue'
alias gra='git rebase --abort'

# Advanced functions
function gac() {
    git add -A
    git commit -m "$1"
}

function gacp() {
    git add -A
    git commit -m "$1"
    git push
}

function gnb() {
    git checkout -b "$1"
    git push -u origin "$1"
}

function gclean() {
    git branch --merged | grep -v "\*" | grep -v "main\|master\|develop" | xargs -n 1 git branch -d
}

# Usage:
# gac "feat: add feature"
# gacp "fix: resolve bug"
# gnb "feature/new-branch"
# gclean  # delete merged branches
```

## Shell Keyboard Shortcuts

```bash
# fzf for git (if installed)
# Add to ~/.bashrc:

# Interactive checkout branch
gcof() {
    local branches branch
    branches=$(git branch -a) &&
    branch=$(echo "$branches" | fzf +m) &&
    git checkout $(echo "$branch" | sed "s/.* //" | sed "s#remotes/[^/]*/##")
}

# Interactive git log
glf() {
    git log --oneline --graph --color=always --all |
    fzf --ansi --no-sort --reverse --tiebreak=index --preview \
    'grep -o "[a-f0-9]\{7,\}" <<< {} | head -1 | xargs git show --color=always' \
    --bind "enter:execute(grep -o '[a-f0-9]\{7,\}' <<< {} | head -1 | xargs git show | less -R)"
}
```

## Best Practices

### Commits

1. **Small, atomic commits** - one commit = one logical change
2. **Good commit message** - clearly describe WHAT and WHY
3. **Commit often** - easier to return to previous state
4. **Test before commit** - don't commit broken code

### Branches

1. **Short-lived feature branches** - merge often
2. **Name consistently** - `feature/`, `bugfix/`, `hotfix/`
3. **Delete merged branches** - maintain order
4. **One branch = one feature**

### Remote

1. **Pull before push** - always update locally
2. **Rebase instead of merge** - cleaner history
3. **Force push carefully** - use `--force-with-lease`
4. **Don't rebase public branches** - only local/feature branches

### History

1. **Clean history** - use rebase and squash
2. **Sensible messages** - not "WIP", "fix", "update"
3. **Interactive rebase before PR** - organize commits
4. **Don't change history after push** - unless feature branch

## Troubleshooting

### Accidentally deleted commit

```bash
git reflog
git checkout commit-hash
git checkout -b recovery
```

### I have conflicts during rebase

```bash
# Resolve conflicts in files
git add resolved-files
git rebase --continue

# Or skip this commit
git rebase --skip

# Or cancel entire rebase
git rebase --abort
```

### I want to undo git push

```bash
# If nobody pulled yet
git reset --hard HEAD~1
git push --force-with-lease

# If others already pulled - use revert
git revert HEAD
git push
```

### I committed sensitive data

```bash
# Remove file and rewrite history
git rm --cached secrets.txt
echo "secrets.txt" >> .gitignore
git commit --amend --no-edit

# Or for older commits
git filter-branch --tree-filter 'rm -f secrets.txt' HEAD

# Or use git-filter-repo (recommended)
git-filter-repo --path secrets.txt --invert-paths
```

## Resources

- `git help <command>` - command documentation
- `man git` - full documentation
- https://git-scm.com/docs - official documentation
- https://learngitbranching.js.org/ - interactive learning

---

## Quick Reference Card

```bash
# Basics
git init                    # new repo
git clone <url>             # clone repo
git status                  # status
git add <file>              # stage
git commit -m "msg"         # commit
git push                    # send to remote
git pull                    # fetch from remote

# Branches
git branch                  # list
git checkout -b <name>      # new branch
git merge <branch>          # merge
git branch -d <name>        # delete

# History
git log                     # history
git log --oneline          # short history
git diff                    # changes
git show <commit>          # show commit

# Undoing
git reset --soft HEAD~1     # undo commit
git restore <file>          # undo changes
git revert <commit>         # revert commit

# Stash
git stash                   # stash
git stash pop              # restore

# Remote
git remote -v              # list remotes
git fetch                  # fetch changes
git push -u origin main    # push with tracking
```
