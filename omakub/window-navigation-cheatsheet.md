# Cheatsheet - Window Navigation

## Basic Window Shortcuts (GNOME/Ubuntu)

### Window Management
- `Super + ←/→` - Snap window to left/right side of screen
- `Super + ↑` - Maximize window
- `Super + ↓` - Restore/minimize window
- `Alt + F4` - Close window
- `Alt + F10` - Toggle window maximization
- `Alt + F8` - Resize window (with arrow keys)
- `Alt + F7` - Move window (with arrow keys)
- `Alt + Space` - Window menu

### Switching Between Windows
- `Alt + Tab` - Switch between windows
- `Alt + Shift + Tab` - Switch between windows (backwards)
- `Alt + \`` (backtick) - Switch between windows of the same application
- `Super + Tab` - Switch between applications (with preview)
- `Ctrl + Alt + Tab` - Switch focus between panels and windows

### Workspaces
- `Super + Page Up/Down` - Switch between workspaces
- `Ctrl + Alt + ↑/↓` - Switch between workspaces (alternative)
- `Super + Shift + Page Up/Down` - Move window to another workspace
- `Ctrl + Alt + Shift + ↑/↓` - Move window to another workspace (alternative)

### Multi-Monitor
- `Super + Shift + ←/→` - Move window to left/right monitor
- `Super + P` - Projector/display settings (show monitor options)
- `Alt + F7` then `Shift + ←/→` - Move window between monitors (after activating move mode)

**Methods to move window between monitors:**

1. **Keyboard shortcut (fastest method):**
   - `Super + Shift + ←` - Move to left monitor
   - `Super + Shift + →` - Move to right monitor

2. **Drag with mouse:**
   - Grab the title bar and drag
   - Tip: hold `Super` while dragging for smoother movement

3. **Window menu:**
   - `Alt + Space` → select "Move to display..." → choose monitor

4. **Via GNOME Settings:**
   - Go to `Settings` → `Displays` to configure monitor positions
   - Proper configuration makes dragging windows easier

**Multi-monitor best practices:**
- Set a primary monitor - new windows will appear there
- Use different workspaces on each monitor for better organization
- Consistently place specific types of applications on specific monitors
  - Example: code on left, documentation on right
  - Example: terminal on main, logs/monitoring on secondary

### Overview and Search
- `Super` - Open Activities Overview (view all windows)
- `Super + A` - Show applications
- `Super + S` - Quick overview of all workspaces

## Terminal Multiplexer (tmux)

### Sessions
- `tmux new -s name` - Create new session
- `tmux ls` - List sessions
- `tmux attach -t name` - Attach to session
- `Ctrl + B, D` - Detach from session
- `Ctrl + B, $` - Rename session

### Windows
- `Ctrl + B, C` - Create new window
- `Ctrl + B, N` - Next window
- `Ctrl + B, P` - Previous window
- `Ctrl + B, 0-9` - Go to window by number
- `Ctrl + B, ,` - Rename window
- `Ctrl + B, &` - Close window (with confirmation)
- `Ctrl + B, W` - List windows (interactive)

### Panes
- `Ctrl + B, %` - Split vertically
- `Ctrl + B, "` - Split horizontally
- `Ctrl + B, ←/→/↑/↓` - Switch between panes
- `Ctrl + B, O` - Next pane (cyclically)
- `Ctrl + B, Q` - Show pane numbers
- `Ctrl + B, X` - Close pane
- `Ctrl + B, Z` - Toggle pane zoom (fullscreen/restore)
- `Ctrl + B, Space` - Change pane layout
- `Ctrl + B, {` - Swap pane with previous
- `Ctrl + B, }` - Swap pane with next
- `Ctrl + B, Ctrl + ←/→/↑/↓` - Resize pane

### Additional
- `Ctrl + B, [` - Copy/scroll mode (q to exit)
- `Ctrl + B, :` - tmux command line
- `Ctrl + B, T` - Show clock

## Screen (Alternative to tmux)

- `Ctrl + A, C` - New window
- `Ctrl + A, N` - Next window
- `Ctrl + A, P` - Previous window
- `Ctrl + A, "` - List windows
- `Ctrl + A, D` - Detach
- `Ctrl + A, |` - Split vertically
- `Ctrl + A, S` - Split horizontally
- `Ctrl + A, Tab` - Switch between panes

## Best Practices

### Workspace Organization
1. **Dedicated workspaces for different tasks**
   - Workspace 1: Browser and communication
   - Workspace 2: Terminal and code
   - Workspace 3: Documentation
   - Workspace 4: Other tools

2. **Name tmux windows**
   - Makes identification and quick switching easier
   - `Ctrl + B, ,` to rename

3. **Group tmux sessions by projects**
   ```bash
   tmux new -s project-frontend
   tmux new -s project-backend
   tmux new -s monitoring
   ```

### Effective Work
1. **Use snap window (Super + ←/→)**
   - Quickly compare documents side-by-side
   - Ideal for code review

2. **Minimize context switching**
   - Keep related windows in the same workspace
   - Use tmux for terminals instead of multiple separate windows

3. **Keyboard shortcuts > mouse**
   - Learn the basic shortcuts
   - Save time and concentration

4. **tmux sessions for long-running tasks**
   - You can detach and return later
   - Survive SSH restart
   - Preserve state of all processes

### Workflow with tmux
```bash
# Standard development workflow
# Window 1: Editor (vim/nano)
# Window 2: Development server
# Window 3: Git and tests
# Window 4: Log monitoring
```

### tmux Customization
Add to `~/.tmux.conf`:
```bash
# Easier pane navigation (without Ctrl+B)
bind -n M-Left select-pane -L
bind -n M-Right select-pane -R
bind -n M-Up select-pane -U
bind -n M-Down select-pane -D

# Start numbering from 1 (easier on keyboard)
set -g base-index 1
setw -g pane-base-index 1

# Faster prefix (optional)
# set -g prefix C-a
# unbind C-b
# bind C-a send-prefix
```

## Quick Commands

### Creating Work Environment
```bash
# New session with window split into 3 panes
tmux new-session \; \
  split-window -h \; \
  split-window -v \; \
  select-pane -t 0
```

### Save and Restore Sessions (tmux-resurrect)
```bash
# Installation
git clone https://github.com/tmux-plugins/tmux-resurrect ~/.tmux/plugins/tmux-resurrect

# In ~/.tmux.conf add:
# run-shell ~/.tmux/plugins/tmux-resurrect/resurrect.tmux

# Save: Ctrl + B, Ctrl + S
# Restore: Ctrl + B, Ctrl + R
```

## Useful Aliases

Add to `~/.bashrc` or `~/.zshrc`:
```bash
alias tl='tmux ls'
alias ta='tmux attach -t'
alias tn='tmux new -s'
alias tk='tmux kill-session -t'
```

## Troubleshooting

### Getting lost in windows?
- Use `Ctrl + B, W` in tmux to see interactive list
- Name all windows (especially in tmux)
- Use no more than 4-5 windows per session

### Too many panes?
- `Ctrl + B, Z` to focus on one pane
- Consider separate windows instead of many panes
- Maximum 3-4 panes in one window

### Shortcut conflicts?
- Check `dconf-editor` for GNOME
- Customize prefix in tmux if it collides with other shortcuts
- Document your changes

## Resources

- [tmux cheatsheet](https://tmuxcheatsheet.com/)
- [GNOME Keyboard Shortcuts](https://help.gnome.org/users/gnome-help/stable/shell-keyboard-shortcuts.html)
- `man tmux` - Full tmux documentation
- `tmux list-keys` - List all bindings in tmux
