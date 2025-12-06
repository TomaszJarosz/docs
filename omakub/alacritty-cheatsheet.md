# Alacritty - Cheatsheet

## Basic Information

Alacritty is a fast, minimalist terminal emulator written in Rust. It features:
- GPU acceleration for maximum performance
- Minimalist design (no built-in tabs/panels)
- YAML file configuration
- Cross-platform (Linux, macOS, Windows)

## Window Management

### Basic Operations
- `Ctrl + Shift + N` - New Alacritty window
- `Ctrl + Shift + Enter` - New window (alternative, depends on configuration)
- `Ctrl + Shift + Q` - Close window
- `Ctrl + D` - Close terminal (exit shell)
- From terminal: `alacritty` - Open new window
- `alacritty --working-directory /path` - Open in specific directory
- `alacritty -e vim file.txt` - Open and execute command

### Fullscreen Mode
- `F11` - Toggle fullscreen mode (depends on configuration)
- Can be configured in `~/.config/alacritty/alacritty.yml`

## Scrolling and Navigation

### Vi Mode (Scrolling/Copying)
- `Ctrl + Shift + Space` - Enter vi mode

**In vi mode:**
- `k` or `↑` - Scroll up (line)
- `j` or `↓` - Scroll down (line)
- `Ctrl + U` - Scroll up (half page)
- `Ctrl + D` - Scroll down (half page)
- `Ctrl + B` - Scroll up (full page)
- `Ctrl + F` - Scroll down (full page)
- `g` - Jump to beginning of history
- `G` - Jump to end (latest output)
- `h/l` - Left/right
- `w/b` - Next/previous word
- `0/$` - Beginning/end of line

**Selection and copying:**
- `v` - Selection (visual mode, character)
- `V` - Line selection (visual line mode)
- `Ctrl + V` - Block selection (visual block)
- `y` - Copy selection to clipboard
- `/` - Search forward
- `?` - Search backward
- `n/N` - Next/previous match
- `Esc` or `q` - Exit vi mode

### Search
- `Ctrl + Shift + F` - Open search bar
- `Enter` - Next match
- `Shift + Enter` - Previous match
- `Esc` - Close search

### Clipboard
- `Ctrl + Shift + C` - Copy selection to clipboard
- `Ctrl + Shift + V` - Paste from clipboard
- `Shift + Insert` - Paste from clipboard (alternative)
- Mouse selection automatically copies (optional, depends on configuration)

## Font and Appearance

### Font Size
- `Ctrl + =` or `Ctrl + +` - Increase font size
- `Ctrl + -` - Decrease font size
- `Ctrl + 0` - Reset font size to default

## URL and Path Interaction

- `Ctrl + Shift + B` - Open URL under cursor in default browser
- `Ctrl + Click` - Open URL (depends on configuration)
- Hints mode (requires configuration):
  - Displays numbers next to URLs/paths
  - Type number to open

## Configuration

### Configuration File Location
```bash
~/.config/alacritty/alacritty.yml
# or
~/.config/alacritty/alacritty.toml  # newer versions
```

### Configuration Reload
- Alacritty automatically reloads configuration after saving
- No need to restart terminal
- If problems occur: close and reopen

### Basic Configuration

```yaml
# ~/.config/alacritty/alacritty.yml

# Window
window:
  opacity: 0.95
  padding:
    x: 10
    y: 10
  decorations: full  # full, none, transparent, buttonless
  startup_mode: Windowed  # Windowed, Maximized, Fullscreen

# Font
font:
  normal:
    family: "JetBrainsMono Nerd Font"
    style: Regular
  bold:
    family: "JetBrainsMono Nerd Font"
    style: Bold
  italic:
    family: "JetBrainsMono Nerd Font"
    style: Italic
  size: 12.0

# Colors (Tokyo Night example)
colors:
  primary:
    background: '#1a1b26'
    foreground: '#c0caf5'
  normal:
    black:   '#15161e'
    red:     '#f7768e'
    green:   '#9ece6a'
    yellow:  '#e0af68'
    blue:    '#7aa2f7'
    magenta: '#bb9af7'
    cyan:    '#7dcfff'
    white:   '#a9b1d6'

# Scrolling
scrolling:
  history: 10000
  multiplier: 3

# Cursor
cursor:
  style:
    shape: Block  # Block, Underline, Beam
    blinking: On
  blink_interval: 750

# Key bindings
key_bindings:
  - { key: Return, mods: Control|Shift, action: SpawnNewInstance }
  - { key: N, mods: Control|Shift, action: SpawnNewInstance }
  - { key: F11, action: ToggleFullscreen }
```

## Best Practices

### Workflow with Alacritty

**1. Alacritty + tmux (Recommended)**
```bash
# One Alacritty window, multiple tmux sessions
alacritty -e tmux new-session -A -s main
```
- Alacritty for system window management
- tmux for session/panel management inside

**2. Multiple Alacritty Windows**
```bash
# Different windows for different tasks
alacritty --working-directory ~/projects/frontend &
alacritty --working-directory ~/projects/backend &
alacritty -e htop &
```

**3. Alacritty on Different Workspaces**
- Workspace 1: Alacritty with editor (vim/nvim)
- Workspace 2: Alacritty with development servers
- Workspace 3: Alacritty with monitoring (htop, logs)

### Performance Optimization

1. **GPU Rendering**
   - Alacritty uses GPU by default
   - Check: `alacritty --print-events`

2. **Font Rendering**
   - Use Nerd Font fonts for icons
   - Disable ligatures if not needed

3. **Scrollback History**
   - Limit `scrolling.history` if you use lots of output
   - 10000 lines is a good balance

### System Integration

**Desktop Entry (Launcher)**
```bash
# ~/.local/share/applications/alacritty-custom.desktop
[Desktop Entry]
Type=Application
Name=Alacritty (Project)
Exec=alacritty --working-directory ~/projects
Icon=Alacritty
Categories=System;TerminalEmulator;
```

**Helper Scripts**
```bash
# ~/bin/alacritty-here
#!/bin/bash
# Open Alacritty in current directory
alacritty --working-directory "$(pwd)" &

# Add to ~/.bashrc:
# alias ah='~/bin/alacritty-here'
```

## Comparison with Other Emulators

| Feature | Alacritty | GNOME Terminal | Kitty | Terminator |
|---------|-----------|----------------|-------|------------|
| GPU Accel | ✓ | ✗ | ✓ | ✗ |
| Tabs | ✗ | ✓ | ✓ | ✗ |
| Panels | ✗ | ✗ | ✓ | ✓ |
| Config | YAML | GUI | Conf | GUI |
| Speed | Fastest | Medium | Fast | Medium |
| Memory | Low | Medium | Medium | Higher |

**Why Alacritty?**
- Maximum speed (GPU rendering)
- Minimalism (no bloat)
- Stability and predictability
- Excellent integration with tmux

**When NOT to use Alacritty?**
- You need built-in tabs (use Kitty)
- You want GUI for configuration (use GNOME Terminal)
- You need built-in panels (use Terminator or Kitty)

## Troubleshooting

### No Colors in Programs
```bash
# Check TERM
echo $TERM  # should be: alacritty or xterm-256color

# If problems, in ~/.bashrc:
export TERM=xterm-256color
```

### Font Problems
```bash
# List available fonts
fc-list | grep -i "font name"

# Install Nerd Fonts
# https://www.nerdfonts.com/
```

### Alacritty Won't Start
```bash
# Check logs
alacritty -v  # verbose mode

# Test configuration
alacritty --config-file ~/.config/alacritty/alacritty.yml
```

### Keyboard Shortcuts Not Working
- Check conflicts with system (GNOME shortcuts)
- Define your own in `key_bindings` in config
- Use `alacritty --print-events` to see captured events

## Useful Commands

```bash
# Version information
alacritty --version

# Check all options
alacritty --help

# Open in debug mode
alacritty -vvv

# Test configuration without affecting running instances
alacritty --config-file /tmp/test-config.yml

# Print default configuration
alacritty migrate  # migrates old configuration to new
```

## Resources

- [Official documentation](https://github.com/alacritty/alacritty)
- [Configuration examples](https://github.com/alacritty/alacritty/blob/master/alacritty.yml)
- [Color schemes](https://github.com/alacritty/alacritty-theme)
- [Nerd Fonts](https://www.nerdfonts.com/)
- `man alacritty` - Manual page
- `man alacritty-msg` - IPC messaging

## Shortcuts - Quick Reference

| Action | Shortcut |
|-------|-------|
| New window | `Ctrl + Shift + N` |
| Close | `Ctrl + Shift + Q` |
| Vi mode | `Ctrl + Shift + Space` |
| Search | `Ctrl + Shift + F` |
| Copy | `Ctrl + Shift + C` |
| Paste | `Ctrl + Shift + V` |
| Zoom in | `Ctrl + =` |
| Zoom out | `Ctrl + -` |
| Reset zoom | `Ctrl + 0` |
| Open URL | `Ctrl + Shift + B` |
