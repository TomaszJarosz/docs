# Omakub Cheatsheet

Omakub is a complete Ubuntu setup from Basecamp - a curated collection of tools and configurations for productive work.

**Official website:** https://omakub.org/

## Omakub Components

- **Terminal:** Zellij (multiplexer)
- **Editor:** Neovim with LazyVim
- **Launcher:** Ulauncher
- **Shell:** Bash with configuration
- **Tools:** fzf, ripgrep, eza, bat, lazygit and more

## Launcher - Ulauncher

**Main shortcut:** `Super+Space` (Windows key + Space)

### Basic Usage
| Action | How |
|--------|-----|
| Open launcher | `Super+Space` |
| Launch application | Type name → `Enter` |
| Search Google | `g query` |
| Calculator | Type expression e.g. `2+2` |

### Available Shortcuts in Launcher
- `g <query>` - Google search
- `gh <repo>` - Open repo on GitHub
- `so <query>` - Stack Overflow search
- `wiki <query>` - Wikipedia search

### Ulauncher Configuration
```bash
# Open settings
ulauncher-toggle
# Then: tray icon → Preferences
```

## Terminal - Zellij

**Launch:**
```bash
zellij
```

### Essential Shortcuts
| Shortcut | Action |
|----------|--------|
| `Alt+h/j/k/l` | Navigate between panes |
| `Alt+n` | New pane |
| `Alt+f` | Floating pane |
| `Alt++/-` | Resize pane |
| `Ctrl+g` | Unlock (normal mode) |

**See details:** `~/docs/zellij-cheatsheet.md`

## Editor - Neovim (LazyVim)

**Launch:**
```bash
nvim file.txt
# or
e file.txt  # alias in Omakub
```

### Essential Shortcuts
| Shortcut | Action |
|----------|--------|
| `Space` | Leader menu (which-key) |
| `Space+ff` | Find files |
| `Space+sg` | Search in files (grep) |
| `Space+e` | File explorer |
| `Esc` | Normal mode |

**See details:** `~/docs/neovim-lazyvim-cheatsheet.md`

## CLI Tools (Omakub Defaults)

### eza (better ls)

Omakub sets up aliases for `ls`:
```bash
ls          # eza with colors
ll          # eza -lh (long list)
la          # eza -lah (all files)
lt          # eza --tree (tree view)
```

### bat (better cat)

```bash
bat file.txt          # Syntax highlighting
bat file1 file2       # Multiple files
bat --style=plain     # No decorations
```

### fzf (fuzzy finder)

```bash
# Interactive file search
Ctrl+T

# Interactive command history
Ctrl+R

# Change directory
Alt+C   # or cd **<Tab>
```

### ripgrep (rg - fast grep)

```bash
rg "pattern"              # Search in files
rg "pattern" --type py    # Only Python files
rg "pattern" -i           # Case insensitive
rg "pattern" -l           # Only file names
```

### lazygit (Git GUI in terminal)

```bash
lazygit
```

**In lazygit:**
| Shortcut | Action |
|----------|--------|
| `1-5` | Switch between panels |
| `Space` | Stage/unstage |
| `c` | Commit |
| `P` | Push |
| `p` | Pull |
| `a` | Amend commit |
| `e` | Edit file |
| `o` | Open file |
| `d` | Delete |
| `q` | Quit |

## Bash Aliases (Omakub)

Check available aliases:
```bash
alias
```

### Most Common
```bash
# Navigation
..          # cd ..
...         # cd ../..
....        # cd ../../..

# Git
g           # git
gs          # git status
ga          # git add
gc          # git commit
gp          # git push
gl          # git pull
gd          # git diff
glog        # git log --oneline --graph

# Editor
e           # nvim
vim         # nvim

# System
update      # sudo apt update && sudo apt upgrade
ports       # netstat -tulanp
myip        # curl ifconfig.me

# Docker (if installed)
dc          # docker-compose
```

## Keyboard Shortcuts (Desktop)

### Window Management
| Shortcut | Action |
|----------|--------|
| `Super+Space` | Ulauncher |
| `Super+Enter` | Terminal |
| `Super+Q` | Close window |
| `Super+F` | Fullscreen |
| `Super+H/L` | Tile left/right |
| `Super+↑/↓` | Maximize/Restore |
| `Alt+Tab` | Switch windows |
| `Super+Tab` | Switch applications |

### Workspaces
| Shortcut | Action |
|----------|--------|
| `Super+PgUp/PgDn` | Switch workspace |
| `Super+Shift+PgUp/PgDn` | Move window to workspace |

**Note:** Shortcuts may vary depending on DE (GNOME, KDE, etc.)

## Package Management

### apt (system packages)
```bash
sudo apt update              # Update package list
sudo apt upgrade             # Install updates
sudo apt install package     # Install package
sudo apt remove package      # Remove package
sudo apt autoremove          # Remove unused dependencies
```

### snap
```bash
snap list                    # List installed
snap install package         # Install
snap remove package          # Remove
```

### Programming Languages

**Ruby (rbenv):**
```bash
rbenv versions               # List versions
rbenv install 3.2.0          # Install version
rbenv global 3.2.0           # Set globally
rbenv local 3.2.0            # Set for project
```

**Node.js (nvm - if installed):**
```bash
nvm list                     # List versions
nvm install 20               # Install Node 20
nvm use 20                   # Use Node 20
nvm alias default 20         # Set as default
```

**Python:**
```bash
python3 --version
pip3 install package
python3 -m venv venv         # Virtual environment
source venv/bin/activate
```

## Omakub Configuration

### Configuration Files

```bash
~/.bashrc                    # Bash config
~/.config/zellij/            # Zellij config
~/.config/nvim/              # Neovim config
~/.gitconfig                 # Git config
~/.local/share/omakub/       # Omakub defaults
```

### Customizing Bash
```bash
# Edit ~/.bashrc
nvim ~/.bashrc

# Reload
source ~/.bashrc
```

### Changing Theme

Omakub has predefined themes for terminal and editor.

**Terminal theme:**
```bash
# Check available
ls ~/.local/share/omakub/themes/

# Edit terminal config (depends on terminal)
```

**Neovim theme:**
```bash
# In Neovim
:Lazy
# Find colorscheme and change
```

## Workflow Tips

### 1. Terminal Workflow
```bash
# Launch Zellij with named session
zellij -s project

# In Zellij:
Alt+n              # New pane
Alt+h/j/k/l        # Navigate
Ctrl+g → o → d     # Detach

# Return later
zellij attach project
```

### 2. Editing with Neovim
```bash
# Open project
cd ~/project
e .                # Open nvim in directory

# In Neovim:
Space+e            # File explorer
Space+ff           # Find file
Space+sg           # Search in files
```

### 3. Git Workflow
```bash
# In project directory
lazygit            # Open lazygit

# Or traditionally:
gs                 # git status
ga .               # git add .
gc -m "message"    # git commit
gp                 # git push
```

### 4. Quick Search
```bash
# Find file
Ctrl+T             # fzf file search

# Search history
Ctrl+R             # fzf command history

# Search in files
rg "pattern"       # ripgrep
```

### 5. Multi-project with Zellij
```bash
# Project 1
zellij -s backend

# Project 2 (new terminal session)
zellij -s frontend

# List sessions
zellij list-sessions

# Switch
Ctrl+g → o → w     # Session manager in Zellij
```

## Customizing Omakub

### Add Custom Aliases
```bash
# Edit ~/.bashrc
nvim ~/.bashrc

# Add at the end:
alias myalias='command'

# Reload
source ~/.bashrc
```

### Add Custom Functions
```bash
# In ~/.bashrc
function mkcd() {
    mkdir -p "$1" && cd "$1"
}

# Usage:
mkcd new-folder
```

### Install Additional Tools
```bash
# Example: tldr (simplified man pages)
sudo apt install tldr
tldr ls

# Example: httpie (HTTP client)
sudo apt install httpie
http GET https://api.github.com
```

## System Maintenance

### System Update
```bash
# Full update
sudo apt update && sudo apt upgrade -y

# Cleanup
sudo apt autoremove
sudo apt autoclean
```

### Checking Disk Space
```bash
df -h              # Partitions
du -sh *           # Folder sizes
ncdu               # Interactive (if installed)
```

### System Monitoring
```bash
htop               # Process monitor
btop               # Modern htop (if installed)
free -h            # Memory
```

## Troubleshooting

### Terminal not opening
```bash
# Check default shell
echo $SHELL

# Reset terminal
Ctrl+C or Ctrl+D
```

### Zellij frozen
```bash
# Kill all sessions
zellij delete-all-sessions

# Clear cache
rm -rf ~/.cache/zellij
```

### Neovim running slow
```bash
# In Neovim
:Lazy
# Update plugins: U

# Check LSP
:LspInfo

# Restart Neovim
:q
nvim
```

### Ulauncher not working
```bash
# Restart Ulauncher
ulauncher-toggle

# Check process
ps aux | grep ulauncher

# Start again
ulauncher &
```

### F11 requires Fn key (Fullscreen issue)

If you need to press `Fn+F11` instead of just `F11`:

**Option 1: Change in BIOS (recommended)**
1. Restart → enter BIOS (F2/F10/Del during startup)
2. Find "Function Key Behavior" or "Action Keys Mode"
3. Change to "Function Keys" (instead of "Multimedia Keys")
4. Save and exit

**Option 2: Use alternative shortcuts**
- `Super+↑` - maximize window
- `Super+F` - fullscreen (in some DEs)

**Option 3: Change shortcut in terminal**
- Open terminal settings
- Keyboard shortcuts
- Change fullscreen to another shortcut (e.g. `Ctrl+Shift+F`)

## Productivity Shortcuts

### 1. Quick Config Editing
```bash
# Bash config
e ~/.bashrc

# Zellij config
e ~/.config/zellij/config.kdl

# Git config
e ~/.gitconfig
```

### 2. Quick Navigation
```bash
# Jump to directories (z)
z project          # Jump to ~/projects/project
                   # (requires 'z' or 'zoxide' installed)

# Marks (bookmarks)
# Add to ~/.bashrc:
export MARKPATH=$HOME/.marks
function jump { cd -P "$MARKPATH/$1" 2>/dev/null || echo "No such mark: $1"; }
function mark { mkdir -p "$MARKPATH"; ln -s "$(pwd)" "$MARKPATH/$1"; }
function unmark { rm -i "$MARKPATH/$1"; }
function marks { ls -l "$MARKPATH" | tail -n +2 | cut -d' ' -f9- ; }
```

### 3. Clipboard Magic
```bash
# Copy output to clipboard
command | xclip -selection clipboard

# Or (if installed)
command | pbcopy   # macOS style

# Alias in ~/.bashrc:
alias c='xclip -selection clipboard'

# Usage:
cat file.txt | c
```

## Resources

- **Omakub Docs:** https://omakub.org/
- **Omakub GitHub:** https://github.com/basecamp/omakub
- **Zellij Docs:** https://zellij.dev/
- **LazyVim Docs:** https://www.lazyvim.org/
- **Ubuntu Docs:** https://help.ubuntu.com/

---

## Quick Start

**First day with Omakub:**

1. **Launch terminal:**
   ```bash
   Super+Enter
   ```

2. **Zellij session:**
   ```bash
   zellij -s work
   ```

3. **Split pane:**
   ```bash
   Alt+n           # New pane
   Alt+h/j/k/l     # Move around
   ```

4. **Open project:**
   ```bash
   cd ~/project
   e .             # Neovim
   ```

5. **Launcher:**
   ```bash
   Super+Space
   ```

6. **Git workflow:**
   ```bash
   lazygit
   ```

**Remember:**
- `Super+Space` - launch anything (Ulauncher)
- `Alt+...` - control Zellij
- `Space` - leader in Neovim
- `Ctrl+R` - command history
- `Ctrl+T` - find file

**Have fun!**
