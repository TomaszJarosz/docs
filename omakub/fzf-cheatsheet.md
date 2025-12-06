# fzf - Fuzzy Finder Cheatsheet

fzf is a powerful fuzzy finder for the command line - it allows you to quickly search for files, commands, processes and much more.

## Basics

### Installation and Configuration (Omakub)

In Omakub fzf is already installed and configured!

**Check version:**
```bash
fzf --version
```

**Configuration (optional):**
Add to `~/.bashrc`:
```bash
# fzf theme
export FZF_DEFAULT_OPTS="--height 40% --layout=reverse --border --inline-info"

# Use ripgrep instead of find
export FZF_DEFAULT_COMMAND='rg --files --hidden --follow --glob "!.git/*"'

# For Ctrl+T
export FZF_CTRL_T_COMMAND="$FZF_DEFAULT_COMMAND"

# For Alt+C
export FZF_ALT_C_COMMAND='fd --type d --hidden --follow --exclude .git'
```

## Built-in Keyboard Shortcuts

Omakub configures these shortcuts automatically:

### Ctrl+T - Fuzzy File Search

```bash
# Press Ctrl+T in command line
vim <Ctrl+T>
# Interactive finder will appear
# Select file(s) and press Enter
# Path will be pasted into command line
```

**Examples:**
```bash
vim <Ctrl+T>              # Open file in vim
cat <Ctrl+T>              # Display file
code <Ctrl+T>             # Open in VSCode
rm <Ctrl+T>               # Delete file (careful!)
```

### Ctrl+R - Command History Search

```bash
# Press Ctrl+R
# Type part of a command
# Fuzzy search in history
# Enter to execute or Tab to edit
```

Much better than the default Ctrl+R in bash!

### Alt+C - Directory Jump

```bash
# Press Alt+C
# Fuzzy search directories
# Enter to CD to selected
```

**Tip:** Combine with `z` or `zoxide` for super fast navigation!

## Navigation in fzf

When fzf is open:

| Shortcut | Action |
|-------|-------|
| `↑/↓` or `Ctrl+k/j` | Up/down |
| `Ctrl+u/d` | Page up/down |
| `Tab` | Select/deselect (multi-select) |
| `Shift+Tab` | Deselect/select |
| `Ctrl+a` | Select all |
| `Ctrl+d` | Deselect all |
| `Enter` | Accept selection |
| `Esc` or `Ctrl+c` | Cancel |
| `Ctrl+/` | Toggle preview window |
| `Shift+↑/↓` | Scroll preview |
| `?` | Toggle preview |

## Basic CLI Usage

### 1. Simple Fuzzy Find

```bash
# Find and list file
find * -type f | fzf

# With ripgrep (faster)
rg --files | fzf

# With fd (more modern)
fd | fzf
```

### 2. Interactive Selection

```bash
# Select file and open in vim
vim $(fzf)

# Select directory and cd
cd $(find . -type d | fzf)

# Better with fd:
cd $(fd -t d | fzf)
```

### 3. Preview Window

```bash
# Preview files with bat
fzf --preview 'bat --color=always {}'

# Preview with line numbers
fzf --preview 'bat -n --color=always {}'

# Preview directories
fzf --preview 'ls -la {}'

# Preview with tree
fzf --preview 'tree -C {}'
```

### 4. Multi-Select

```bash
# Select multiple files (Tab)
vim $(fzf -m)

# Delete multiple files
rm $(fzf -m)

# Add to git
git add $(fzf -m)
```

## Advanced Usage

### Filtering and Options

```bash
# Exact match (prefix ')
fzf -q "'exact"

# Exact suffix match ($)
fzf -q "txt$"

# Prefix match (^)
fzf -q "^src"

# Negation (!)
fzf -q "!test"

# OR (|)
fzf -q "jpg$ | png$"

# AND (space)
fzf -q "src test"
```

**Query syntax:**
- `'exact` - exact match
- `^prefix` - prefix match
- `suffix$` - suffix match
- `!not` - negation
- `term1 term2` - AND
- `term1 | term2` - OR

### Layout and Appearance

```bash
# Reverse layout (results on top)
fzf --reverse

# With border
fzf --border

# Height
fzf --height 40%
fzf --height 100%

# Position
fzf --layout=reverse
fzf --layout=default

# Inline info
fzf --inline-info

# No mouse
fzf --no-mouse

# Multi-select
fzf -m
fzf --multi
```

## Useful Bash Functions

Add to `~/.bashrc`:

### 1. Quick File Opening

```bash
# fe - Fuzzy Edit (open in editor)
fe() {
    local file
    file=$(fzf --preview 'bat --color=always {}') && nvim "$file"
}

# fcd - Fuzzy CD
fcd() {
    local dir
    dir=$(fd -t d | fzf --preview 'tree -C {} | head -100') && cd "$dir"
}

# fo - Fuzzy Open (xdg-open)
fo() {
    local file
    file=$(fzf --preview 'bat --color=always {}') && xdg-open "$file"
}
```

### 2. Git Integration

```bash
# fgb - Fuzzy Git Branch (checkout)
fgb() {
    git branch -a | grep -v HEAD | \
    fzf --preview 'git log --oneline --graph --date=short --pretty="format:%C(auto)%cd %h%d %s" $(sed "s/.* //" <<< {}) | head -50' | \
    sed "s/.* //" | sed "s#remotes/[^/]*/##" | \
    xargs git checkout
}

# fgs - Fuzzy Git Show (view commit)
fgs() {
    git log --oneline --color=always | \
    fzf --ansi --preview 'git show --color=always {1}' | \
    cut -d ' ' -f 1 | xargs git show
}

# fga - Fuzzy Git Add
fga() {
    git status -s | \
    fzf -m --preview 'git diff --color=always {2}' | \
    awk '{print $2}' | xargs git add
}

# fgd - Fuzzy Git Diff
fgd() {
    git status -s | \
    fzf --preview 'git diff --color=always {2}'
}
```

### 3. Process Management

```bash
# fkill - Fuzzy Kill Process
fkill() {
    local pid
    pid=$(ps -ef | sed 1d | fzf -m | awk '{print $2}')
    if [ "x$pid" != "x" ]; then
        echo $pid | xargs kill -${1:-9}
    fi
}

# Usage: fkill or fkill 15 (SIGTERM)
```

### 4. History Search Enhanced

```bash
# fh - Fuzzy History (better than Ctrl+R)
fh() {
    eval $(history | fzf --tac --no-sort | sed 's/ *[0-9]* *//')
}
```

### 5. Docker Integration

```bash
# fdi - Fuzzy Docker Image
fdi() {
    docker images | fzf --header-lines=1 | awk '{print $3}'
}

# fdc - Fuzzy Docker Container
fdc() {
    docker ps -a | fzf --header-lines=1 | awk '{print $1}'
}

# fdl - Fuzzy Docker Logs
fdl() {
    docker ps -a | fzf --header-lines=1 | awk '{print $1}' | xargs docker logs -f
}

# fdsh - Fuzzy Docker Shell
fdsh() {
    docker ps | fzf --header-lines=1 | awk '{print $1}' | xargs -I {} docker exec -it {} /bin/bash
}
```

### 6. Find and Edit (Ripgrep Integration)

```bash
# frg - Fuzzy Ripgrep (search in file contents)
frg() {
    rg --color=always --line-number --no-heading --smart-case "${*:-}" |
    fzf --ansi \
        --color "hl:-1:underline,hl+:-1:underline:reverse" \
        --delimiter : \
        --preview 'bat --color=always {1} --highlight-line {2}' \
        --preview-window 'up,60%,border-bottom,+{2}+3/3,~3' \
        --bind 'enter:become(nvim {1} +{2})'
}

# Usage: frg "search term"
```

### 7. Man Pages

```bash
# fman - Fuzzy Man Pages
fman() {
    man -k . | fzf --preview 'man {1}' | awk '{print $1}' | xargs man
}
```

### 8. SSH Hosts

```bash
# fssh - Fuzzy SSH
fssh() {
    local host
    host=$(grep -E '^Host ' ~/.ssh/config | sed 's/Host //' | fzf)
    if [ -n "$host" ]; then
        ssh "$host"
    fi
}
```

## Integration with Other Tools

### With Vim/Neovim

**Plugin: fzf.vim**
```vim
" In ~/.config/nvim/init.vim or init.lua
Plug 'junegunn/fzf', { 'do': { -> fzf#install() } }
Plug 'junegunn/fzf.vim'

" Shortcuts:
nnoremap <C-p> :Files<CR>
nnoremap <C-f> :Rg<CR>
nnoremap <leader>b :Buffers<CR>
```

### With Zellij/tmux

```bash
# In Zellij - fuzzy session switch
zellij list-sessions | fzf | xargs zellij attach

# Alias:
alias zs='zellij list-sessions | fzf | xargs zellij attach'
```

### With bat (Better Cat)

```bash
# Preview with bat (syntax highlighting)
export FZF_CTRL_T_OPTS="--preview 'bat -n --color=always {}'"
export FZF_ALT_C_OPTS="--preview 'tree -C {} | head -100'"
```

### With fd (Better Find)

```bash
# Use fd instead of find
export FZF_DEFAULT_COMMAND='fd --type f --hidden --follow --exclude .git'
export FZF_CTRL_T_COMMAND="$FZF_DEFAULT_COMMAND"
export FZF_ALT_C_COMMAND='fd --type d --hidden --follow --exclude .git'
```

## Example Workflows

### 1. Developer Workflow

```bash
# Quickly open project
cd ~/projects
cd $(fd -t d | fzf)

# Find and edit file
vim $(fzf --preview 'bat --color=always {}')

# Search in code and edit
frg "function name"  # Opens nvim at the correct line

# Git commit with fzf
fga  # Fuzzy add files
gc "commit message"
```

### 2. System Administration

```bash
# Check processes and kill
fkill

# View logs
journalctl | fzf

# SSH to server
fssh
```

### 3. File Management

```bash
# Find and delete
rm $(fzf -m)

# Find and copy
cp $(fzf -m) /destination/

# Find and move
mv $(fzf -m) /destination/
```

## Color Configuration

Add to `~/.bashrc`:

```bash
# fzf color scheme (Tokyo Night)
export FZF_DEFAULT_OPTS=$FZF_DEFAULT_OPTS'
  --color=fg:#c0caf5,bg:#1a1b26,hl:#ff9e64
  --color=fg+:#c0caf5,bg+:#292e42,hl+:#ff9e64
  --color=info:#7aa2f7,prompt:#7dcfff,pointer:#7dcfff
  --color=marker:#9ece6a,spinner:#9ece6a,header:#9ece6a'

# Or Catppuccin:
export FZF_DEFAULT_OPTS=$FZF_DEFAULT_OPTS'
  --color=bg+:#313244,bg:#1e1e2e,spinner:#f5e0dc,hl:#f38ba8
  --color=fg:#cdd6f4,header:#f38ba8,info:#cba6f7,pointer:#f5e0dc
  --color=marker:#f5e0dc,fg+:#cdd6f4,prompt:#cba6f7,hl+:#f38ba8'
```

## Complete ~/.bashrc Setup

```bash
# fzf configuration
export FZF_DEFAULT_OPTS="
  --height 40%
  --layout=reverse
  --border
  --inline-info
  --preview-window=:hidden
  --bind '?:toggle-preview'
  --bind 'ctrl-/:toggle-preview'
  --bind 'ctrl-u:preview-page-up'
  --bind 'ctrl-d:preview-page-down'
"

# Use ripgrep
export FZF_DEFAULT_COMMAND='rg --files --hidden --follow --glob "!.git/*"'
export FZF_CTRL_T_COMMAND="$FZF_DEFAULT_COMMAND"
export FZF_ALT_C_COMMAND='fd --type d --hidden --follow --exclude .git'

# Preview
export FZF_CTRL_T_OPTS="--preview 'bat -n --color=always {}'"
export FZF_ALT_C_OPTS="--preview 'tree -C {} | head -100'"

# Functions (add all from "Useful Bash Functions" section above)
fe() { ... }
fcd() { ... }
fgb() { ... }
# etc.
```

## Tips & Tricks

### 1. Exclude Patterns

```bash
# Ignore node_modules, .git, etc
rg --files --hidden --follow \
  -g '!{.git,node_modules,target,dist,build}/*' | fzf
```

### 2. Quick Aliases

```bash
alias f='fzf'
alias ff='fzf --preview "bat --color=always {}"'
alias v='vim $(fzf)'
```

### 3. Pipe to fzf

```bash
# Everything can be piped to fzf!
ls | fzf
history | fzf
docker ps | fzf
kubectl get pods | fzf
```

### 4. Custom Key Bindings

```bash
# In fzf you can define custom actions
fzf --bind 'ctrl-e:execute(nvim {})'
fzf --bind 'ctrl-y:execute-silent(echo {} | xclip)'
```

### 5. Multi-Stage Pipeline

```bash
# Select directory, then file in it
cd $(fd -t d | fzf) && vim $(fzf)
```

## Performance Tips

1. **Use ripgrep/fd instead of find** - much faster
2. **Limit depth** - `fd --max-depth 3`
3. **Exclude large directories** - node_modules, .git, target
4. **Cache file list** for large projects:
```bash
# Generate file list once
fd > /tmp/files.txt
cat /tmp/files.txt | fzf
```

## Troubleshooting

### fzf not finding files

```bash
# Check FZF_DEFAULT_COMMAND
echo $FZF_DEFAULT_COMMAND

# Reset to default
unset FZF_DEFAULT_COMMAND
```

### Shortcuts not working

```bash
# Make sure fzf key bindings are loaded
# Should be in ~/.bashrc:
[ -f ~/.fzf.bash ] && source ~/.fzf.bash
```

### Preview not working

```bash
# Install bat
sudo apt install bat
# or
cargo install bat

# Install tree
sudo apt install tree
```

## Resources

- **fzf GitHub:** https://github.com/junegunn/fzf
- **fzf Wiki:** https://github.com/junegunn/fzf/wiki
- **Advanced Examples:** https://github.com/junegunn/fzf/wiki/examples
- `man fzf` - Documentation
- **Interactive Tutorial:** just start using Ctrl+T/Ctrl+R!

## Quick Start

```bash
# Try built-in:
Ctrl+T     # Fuzzy file search
Ctrl+R     # Fuzzy command history
Alt+C      # Fuzzy directory jump

# Basic usage:
vim $(fzf)
cd $(fd -t d | fzf)
kill $(ps -ef | fzf | awk '{print $2}')

# With preview:
fzf --preview 'bat --color=always {}'
```

**Remember:**
- Everything can be input for fzf (pipe)
- Tab = multi-select
- ? = toggle preview
- fzf + bat + ripgrep + fd = super combo!
