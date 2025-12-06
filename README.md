# Developer Productivity Documentation

A comprehensive collection of cheatsheets, guides, and best practices for modern developer tools and workflows.

## Overview

This repository contains documentation for:
- **Development Environment** - Omakub setup, terminal tools, editors
- **AI-Assisted Coding** - Claude Code configuration and usage patterns
- **Productivity Tools** - Git workflows, IDE shortcuts, editor guides
- **System Configuration** - Linux customization and fixes

## Quick Start

| Tool | Cheatsheet | Description |
|------|------------|-------------|
| Omakub | [omakub-cheatsheet](omakub/omakub-cheatsheet.md) | Complete Ubuntu development environment |
| Zellij | [zellij-cheatsheet](omakub/zellij-cheatsheet.md) | Modern terminal multiplexer |
| Neovim | [neovim-lazyvim-cheatsheet](omakub/neovim-lazyvim-cheatsheet.md) | Modal text editor with LazyVim |
| fzf | [fzf-cheatsheet](omakub/fzf-cheatsheet.md) | Fuzzy finder for terminal |
| Claude Code | [claude-code-config](claude/claude-code-config-cheatsheet.md) | AI coding assistant configuration |

## Directory Structure

```
docs/
├── README.md                     # This file
├── omakub/                       # Omakub environment tools
│   ├── omakub-cheatsheet.md      # Main Omakub overview
│   ├── shell-productivity-cheatsheet.md
│   ├── git-lazygit-cheatsheet.md
│   ├── fzf-cheatsheet.md
│   ├── neovim-lazyvim-cheatsheet.md
│   ├── zellij-cheatsheet.md
│   ├── alacritty-cheatsheet.md
│   ├── omakub-webapps-guide.md
│   └── window-navigation-cheatsheet.md
├── claude/                       # Claude Code AI assistant
│   ├── claude-code-config-cheatsheet.md
│   └── claude-code-usage-tips.md
├── tools/                        # Development tools
│   ├── git-console-cheatsheet.md
│   ├── intellij-keyboard-productivity.md
│   └── neovim-productivity-guide.md
└── system/                       # System configuration
    └── keyboard-remapping-fix.md
```

## Documentation Categories

### Omakub Environment

[Omakub](https://omakub.org/) is a curated Ubuntu development environment from Basecamp. These guides cover all included tools:

| Guide | Description |
|-------|-------------|
| [Omakub Cheatsheet](omakub/omakub-cheatsheet.md) | Overview of all Omakub tools and workflows |
| [Shell Productivity](omakub/shell-productivity-cheatsheet.md) | Bash shortcuts, aliases, and shell productivity |
| [Git & Lazygit](omakub/git-lazygit-cheatsheet.md) | Git commands and Lazygit terminal UI |
| [fzf Fuzzy Finder](omakub/fzf-cheatsheet.md) | Fuzzy finding for files, history, and more |
| [Neovim/LazyVim](omakub/neovim-lazyvim-cheatsheet.md) | Modal editing with Neovim and LazyVim config |
| [Zellij](omakub/zellij-cheatsheet.md) | Terminal multiplexer with modern UI |
| [Alacritty](omakub/alacritty-cheatsheet.md) | GPU-accelerated terminal emulator |
| [Web Apps](omakub/omakub-webapps-guide.md) | Creating desktop apps from web services |
| [Window Navigation](omakub/window-navigation-cheatsheet.md) | Desktop window and workspace management |

### Claude Code (AI Assistant)

Guides for using Claude Code effectively:

| Guide | Description |
|-------|-------------|
| [Configuration](claude/claude-code-config-cheatsheet.md) | Setup, settings.json, hooks, MCP servers |
| [Usage Tips](claude/claude-code-usage-tips.md) | Best practices, prompting patterns, workflows |

### Development Tools

IDE and tool productivity guides:

| Guide | Description |
|-------|-------------|
| [Git Console](tools/git-console-cheatsheet.md) | Command-line Git workflows and aliases |
| [IntelliJ IDEA](tools/intellij-keyboard-productivity.md) | Keyboard-only IntelliJ productivity |
| [Neovim Guide](tools/neovim-productivity-guide.md) | Deep dive into Vim/Neovim productivity |

### System Configuration

Linux system customization:

| Guide | Description |
|-------|-------------|
| [Keyboard Remapping](system/keyboard-remapping-fix.md) | X11 modifier key remapping fix |

## Essential Shortcuts

### Terminal Navigation
| Shortcut | Action |
|----------|--------|
| `Ctrl+R` | Search command history (fzf) |
| `Ctrl+T` | Find files (fzf) |
| `Alt+C` | Change directory (fzf) |
| `Alt+h/j/k/l` | Navigate Zellij panes |

### Editor (Neovim/LazyVim)
| Shortcut | Action |
|----------|--------|
| `Space` | Leader key (opens which-key menu) |
| `Space+ff` | Find files |
| `Space+sg` | Search in files (grep) |
| `Space+e` | File explorer |

### Desktop
| Shortcut | Action |
|----------|--------|
| `Super+Space` | Ulauncher (app launcher) |
| `Super+Enter` | Open terminal |
| `Super+←/→` | Tile window left/right |
| `Alt+Tab` | Switch windows |

## Usage

Clone this repository or browse individual files:

```bash
# Clone the docs
git clone https://github.com/your-username/docs.git

# Open a cheatsheet
cat docs/omakub/fzf-cheatsheet.md

# Or use your editor
nvim docs/
```

## Contributing

Feel free to:
- Fix typos or errors
- Add missing information
- Improve explanations
- Add new cheatsheets for tools you use

## Resources

### Official Documentation
- [Omakub](https://omakub.org/) - Ubuntu development environment
- [Zellij](https://zellij.dev/) - Terminal multiplexer
- [LazyVim](https://www.lazyvim.org/) - Neovim configuration
- [fzf](https://github.com/junegunn/fzf) - Fuzzy finder
- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) - AI coding assistant

### Learning Resources
- [Vim Adventures](https://vim-adventures.com/) - Learn Vim through games
- [Learn Git Branching](https://learngitbranching.js.org/) - Interactive Git tutorial
- [Vimtutor](https://vimschool.netlify.app/introduction/vimtutor/) - Built-in Vim tutorial

## License

This documentation is provided as-is for educational purposes.

---

**Happy coding!**
