# Zellij Cheatsheet (Omakub Config)

Zellij is a modern terminal multiplexer - an alternative to tmux/screen.

**NOTE:** This configuration is from **Omakub** and differs from the default!

## Basic Concepts

Zellij in Omakub works in **modes** with a key difference:
- **By default you are in LOCKED mode** - most shortcuts are disabled!
- `Ctrl+g` switches between **locked** ↔ **normal** mode
- In locked mode only `Alt+...` shortcuts work (the most important!)
- From normal mode you can enter other modes (pane, tab, resize, etc.)

## ⭐ Most Important Shortcuts (Always Work)

Shortcuts with **Alt** work even in locked mode:

| Shortcut | Action |
|-------|-------|
| `Alt+h/j/k/l` or `Alt+arrows` | Navigate between panes/tabs |
| `Alt+n` | New pane |
| `Alt+f` | Toggle floating panes |
| `Alt++` | Increase pane size |
| `Alt+-` | Decrease pane size |
| `Alt+=` | Increase pane size |
| `Alt+[` | Previous layout |
| `Alt+]` | Next layout |
| `Alt+i` | Move tab left |
| `Alt+o` | Move tab right |

## Basic Shortcuts

### General
| Shortcut | Action |
|-------|-------|
| `Ctrl+g` | Toggle locked ↔ normal mode |
| `Ctrl+q` | Close Zellij (only from normal mode) |

## Modes and Management

**NOTE:** From locked mode first press `Ctrl+g` to enter normal mode!

### Panel Mode (from normal: `p`)
Managing panes (screen splits):

| Full Shortcut | Action |
|-------|-------|
| `Ctrl+g` → `p` → `n` | New pane (default direction) |
| `Ctrl+g` → `p` → `d` | Pane down (horizontal split) |
| `Ctrl+g` → `p` → `r` | Pane right (vertical split) |
| `Ctrl+g` → `p` → `x` | Close active pane |
| `Ctrl+g` → `p` → `f` | **Fullscreen pane** ⭐ |
| `Ctrl+g` → `p` → `w` | Toggle floating pane |
| `Ctrl+g` → `p` → `e` | Embed floating pane |
| `Ctrl+g` → `p` → `c` | Rename pane |
| `Ctrl+g` → `p` → `z` | Toggle pane frames |

**Navigation in Panel Mode:**
| Full Shortcut | Action |
|-------|-------|
| `Ctrl+g` → `p` → `h/←` | Go to pane on the left |
| `Ctrl+g` → `p` → `l/→` | Go to pane on the right |
| `Ctrl+g` → `p` → `j/↓` | Go to pane below |
| `Ctrl+g` → `p` → `k/↑` | Go to pane above |
| `Ctrl+g` → `p` → `Tab` | Toggle focus |

### Resize Mode (from normal: `r`)
Resizing panes:

| Full Shortcut | Action |
|-------|-------|
| `Ctrl+g` → `r` → `h/←` | Increase left |
| `Ctrl+g` → `r` → `l/→` | Increase right |
| `Ctrl+g` → `r` → `j/↓` | Increase down |
| `Ctrl+g` → `r` → `k/↑` | Increase up |
| `Ctrl+g` → `r` → `+` | Increase size |
| `Ctrl+g` → `r` → `-` | Decrease size |
| `Ctrl+g` → `r` → `=` | Increase size (like +) |
| `Ctrl+g` → `r` → `H/J/K/L` | Decrease in given direction |

💡 **Faster way:** Use `Alt++` or `Alt+-` without entering mode!

### Tab Mode (from normal: `t`)
Managing tabs:

| Full Shortcut | Action |
|-------|-------|
| `Ctrl+g` → `t` → `n` | New tab |
| `Ctrl+g` → `t` → `x` | Close active tab |
| `Ctrl+g` → `t` → `r` | Rename tab |
| `Ctrl+g` → `t` → `h/←` | Go to previous tab |
| `Ctrl+g` → `t` → `l/→` | Go to next tab |
| `Ctrl+g` → `t` → `j` | Go to next tab |
| `Ctrl+g` → `t` → `k` | Go to previous tab |
| `Ctrl+g` → `t` → `1-9` | Go to tab number 1-9 |
| `Ctrl+g` → `t` → `Tab` | Switch to last used tab |
| `Ctrl+g` → `t` → `s` | Sync tab (synchronize input) |
| `Ctrl+g` → `t` → `[` | Break pane left |
| `Ctrl+g` → `t` → `]` | Break pane right |
| `Ctrl+g` → `t` → `b` | Break pane |

### Scroll Mode (from normal: `s`)
Scrolling and copying:

| Full Shortcut | Action |
|-------|-------|
| `Ctrl+g` → `s` → `↑/↓` or `k/j` | Scroll up/down |
| `Ctrl+g` → `s` → `PgUp/PgDn` or `h/l` | Scroll by pages |
| `Ctrl+g` → `s` → `u` | Half page up |
| `Ctrl+g` → `s` → `d` | Half page down |
| `Ctrl+g` → `s` → `Ctrl+b` | Page scroll up |
| `Ctrl+g` → `s` → `Ctrl+f` | Page scroll down |
| `Ctrl+g` → `s` → `f` | Search (enter search) |
| `Ctrl+g` → `s` → `e` | Edit scrollback in editor |
| `Ctrl+g` → `s` → `Ctrl+c` | Exit scroll mode |

**In Search Mode:**
| Shortcut | Action |
|-------|-------|
| `n` | Next result |
| `p` | Previous result |
| `c` | Toggle case sensitivity |
| `w` | Toggle whole word |
| `o` | Toggle wrap |

Copying text:
1. Enter Scroll Mode (`Ctrl+g` → `s`)
2. Select text with mouse
3. Text automatically copies to clipboard
4. `Ctrl+c` or `Esc` to exit

### Session Mode (from normal: `o`)
Managing sessions:

| Full Shortcut | Action |
|-------|-------|
| `Ctrl+g` → `o` → `d` | Detach (disconnect from session) |
| `Ctrl+g` → `o` → `w` | Session manager (session list) |
| `Ctrl+g` → `o` → `c` | Configuration plugin |
| `Ctrl+g` → `o` → `p` | Plugin manager |

### Move Mode (from normal: `m`)
Moving panes:

| Full Shortcut | Action |
|-------|-------|
| `Ctrl+g` → `m` → `n` | Move pane (next) |
| `Ctrl+g` → `m` → `p` | Move pane back |
| `Ctrl+g` → `m` → `h/j/k/l` | Move pane in direction |
| `Ctrl+g` → `m` → `arrows` | Move pane in direction |
| `Ctrl+g` → `m` → `Tab` | Move pane |

## Sessions

### Creating and Connecting
```bash
# New session with name
zellij -s session-name

# New session with layout
zellij --layout layout-name

# List sessions
zellij list-sessions

# Attach to session
zellij attach session-name

# Attach to last
zellij attach

# Delete session
zellij delete-session session-name

# Kill all sessions
zellij delete-all-sessions
```

## Layouts

Layouts are in `~/.config/zellij/layouts/`

Example layout (`dev.kdl`):
```kdl
layout {
    pane split_direction="vertical" {
        pane
        pane split_direction="horizontal" {
            pane
            pane
        }
    }
}
```

Launch with layout:
```bash
zellij --layout dev
```

## Configuration

Main file: `~/.config/zellij/config.kdl`

### Useful options
```kdl
// Disable mouse mode
mouse_mode false

// Change default shell
default_shell "fish"

// Copy to system clipboard
copy_command "xclip -selection clipboard"

// Automatic layout
auto_layout true
```

## Floating Panes

| Shortcut | Action |
|-------|-------|
| `Alt+f` | Toggle floating panes (fastest!) ⭐ |
| `Ctrl+g` → `p` → `w` | Toggle floating pane |
| `Ctrl+g` → `p` → `e` | Toggle embedded floating pane |

Floating panes are panels "floating" above others - useful for quick notes, calculator, etc.

## Tips & Tricks (Omakub Edition)

### 1. ⭐ Use Alt shortcuts!
This is the most important tip - **use `Alt`** instead of entering modes:
- `Alt+h/j/k/l` - navigation (instead of `Ctrl+g` → `p` → `h/j/k/l`)
- `Alt+n` - new pane (instead of `Ctrl+g` → `p` → `n`)
- `Alt+f` - floating panes (instead of `Ctrl+g` → `p` → `w`)
- `Alt++/-` - resize (instead of entering resize mode)

### 2. Locked mode is the default mode
- Zellij starts in **locked mode** - this is normal!
- Most shortcuts don't work - this is intentional (to avoid conflicts with programs)
- `Ctrl+g` unlocks when you need advanced features
- Automatically returns to locked mode after action

### 3. Fullscreen for focus
`Ctrl+g` → `p` → `f` - hide other panes and focus on one

### 4. Copying from Zellij
Text selected with mouse in Scroll Mode (`Ctrl+g` → `s`) automatically goes to system clipboard

### 5. Named sessions
Always use names for work sessions:
```bash
zellij -s project-backend
zellij -s project-frontend
```

### 6. Session manager
`Ctrl+g` → `o` → `w` shows all sessions - you can quickly switch between projects

### 7. Edit scrollback
`Ctrl+g` → `s` → `e` opens entire scrollback in nvim - great for copying long outputs

### 8. Layouts for projects
Create a layout for each project with typical pane configuration (compact is default in Omakub)

## Comparison with tmux

| Feature | Zellij (Omakub) | tmux |
|---------|--------|------|
| Unlock/Prefix | `Ctrl+g` (locked↔normal) | `Ctrl+b` |
| Navigation | `Alt+h/j/k/l` ⭐ | `Ctrl+b` → arrows |
| Vertical split | `Ctrl+g` → `p` → `r` | `Ctrl+b` → `%` |
| Horizontal split | `Ctrl+g` → `p` → `d` | `Ctrl+b` → `"` |
| Quick new pane | `Alt+n` ⭐ | none |
| New tab | `Ctrl+g` → `t` → `n` | `Ctrl+b` → `c` |
| Detach | `Ctrl+g` → `o` → `d` | `Ctrl+b` → `d` |
| Scroll | `Ctrl+g` → `s` | `Ctrl+b` → `[` |
| Resize | `Alt++/-` ⭐ | `Ctrl+b` → `:resize-pane` |
| Fullscreen | `Ctrl+g` → `p` → `f` | `Ctrl+b` → `z` |

**Main difference:** Omakub uses "locked by default" + `Alt` shortcuts for common actions!

## Common Problems

### Zellij won't start
```bash
# Check logs
zellij --debug

# Clear cache
rm -rf ~/.cache/zellij
```

### Copying doesn't work
Set in `config.kdl`:
```kdl
copy_command "xclip -selection clipboard"
```

### Font is broken
Install Nerd Font and set in terminal

## Useful Commands

```bash
# Show version
zellij --version

# Run command in new pane
zellij run -- htop

# Run in background (without attaching)
zellij -s background-task run -- long-running-command

# Setup completion (bash)
zellij setup --generate-completion bash > /etc/bash_completion.d/zellij
```

## Resources

- Documentation: https://zellij.dev/documentation
- Repo: https://github.com/zellij-org/zellij
- Community layouts: https://github.com/zellij-org/zellij/discussions

---

## Quick Start (Omakub)

**Simplest workflow:**
1. `zellij` - launch (you start in locked mode)
2. `Alt+n` - new pane ⭐
3. `Alt+h/j/k/l` - move between panes ⭐
4. `Alt++/-` - resize ⭐
5. `Alt+f` - floating pane ⭐

**Advanced features:**
1. `Ctrl+g` - unlock (enter normal mode)
2. `p` → `d` - split pane down
3. `p` → `r` - split pane right
4. `p` → `f` - fullscreen
5. `t` → `n` - new tab
6. `o` → `d` - detach from session
7. `Esc` or `Enter` - return to locked mode

**Remember:**
- 🔒 **Locked mode** = default, most shortcuts disabled
- ⌨️ **Alt+...** = work always, even in locked mode
- 🔓 **Ctrl+g** = toggle locked ↔ normal
- ✅ Automatically returns to locked mode after action
