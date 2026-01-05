# Developer Productivity Documentation

A comprehensive collection of cheatsheets, guides, and best practices for modern developer tools and workflows.

## Overview

This repository contains documentation for:
- **Development Environment** - Omakub setup, terminal tools, editors
- **AI-Assisted Coding** - Claude Code configuration and usage patterns
- **Productivity Tools** - Git workflows, IDE shortcuts, editor guides
- **DevOps** - Docker, SSH, task runners, debugging tools
- **System Configuration** - Linux customization and fixes

## Quick Start

**New here?** Start with the [Quickstart Guide](quickstart.md) to get productive in 10 minutes.

| Tool | Cheatsheet | Description |
|------|------------|-------------|
| Quickstart | [quickstart](quickstart.md) | Get productive in 10 minutes |
| Omakub | [omakub-cheatsheet](omakub/omakub-cheatsheet.md) | Complete Ubuntu development environment |
| Zellij | [zellij-cheatsheet](omakub/zellij-cheatsheet.md) | Modern terminal multiplexer |
| Neovim | [neovim-lazyvim-cheatsheet](omakub/neovim-lazyvim-cheatsheet.md) | Modal text editor with LazyVim |
| fzf | [fzf-cheatsheet](omakub/fzf-cheatsheet.md) | Fuzzy finder for terminal |
| Claude Code | [claude-code-config](claude/claude-code-config-cheatsheet.md) | AI coding assistant configuration |

## Directory Structure

```
docs/
├── README.md                           # This file
├── quickstart.md                       # 10-minute quickstart guide
├── keyboard-shortcuts-index.md         # All shortcuts in one place
├── troubleshooting-faq.md              # Common issues and solutions
│
├── omakub/                             # Omakub environment tools
│   ├── omakub-cheatsheet.md            # Main Omakub overview
│   ├── shell-productivity-cheatsheet.md
│   ├── git-lazygit-cheatsheet.md
│   ├── fzf-cheatsheet.md
│   ├── neovim-lazyvim-cheatsheet.md
│   ├── zellij-cheatsheet.md
│   ├── alacritty-cheatsheet.md
│   ├── omakub-webapps-guide.md
│   └── window-navigation-cheatsheet.md
│
├── claude/                             # Claude Code AI assistant
│   ├── claude-code-config-cheatsheet.md
│   └── claude-code-usage-tips.md
│
├── tools/                              # Development tools
│   ├── git-console-cheatsheet.md       # Advanced Git CLI
│   ├── intellij-keyboard-productivity.md
│   ├── neovim-productivity-guide.md
│   ├── docker-podman-cheatsheet.md     # Containers
│   ├── tmux-cheatsheet.md              # Terminal multiplexer
│   ├── ssh-remote-dev-guide.md         # SSH & remote work
│   ├── debugging-tools-guide.md        # gdb, strace, perf
│   └── task-runners-cheatsheet.md      # Make, Just, Task
│
├── system/                             # System configuration
│   └── keyboard-remapping-fix.md
│
└── mkdocs.yml                          # MkDocs configuration
```

## Documentation Categories

### Getting Started

| Guide | Description |
|-------|-------------|
| [Quickstart](quickstart.md) | Get productive in 10 minutes |
| [Keyboard Shortcuts Index](keyboard-shortcuts-index.md) | All shortcuts from all docs in one place |
| [Troubleshooting FAQ](troubleshooting-faq.md) | Common issues and solutions |

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
| [Usage Tips](claude/claude-code-usage-tips.md) | Best practices, prompting patterns, custom slash commands |

### Development Tools

IDE and tool productivity guides:

| Guide | Description |
|-------|-------------|
| [Git Console](tools/git-console-cheatsheet.md) | Command-line Git workflows, bisect, worktree |
| [IntelliJ IDEA](tools/intellij-keyboard-productivity.md) | Keyboard-only IntelliJ productivity |
| [Neovim Guide](tools/neovim-productivity-guide.md) | Deep dive into Vim/Neovim productivity |
| [tmux](tools/tmux-cheatsheet.md) | Terminal multiplexer (alternative to Zellij) |

### DevOps & Infrastructure

| Guide | Description |
|-------|-------------|
| [Docker & Podman](tools/docker-podman-cheatsheet.md) | Containers, images, Docker Compose |
| [SSH & Remote Dev](tools/ssh-remote-dev-guide.md) | SSH config, tunnels, remote development |
| [Task Runners](tools/task-runners-cheatsheet.md) | Make, Just, Task (go-task) |
| [Debugging Tools](tools/debugging-tools-guide.md) | gdb, strace, ltrace, perf, valgrind |

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

See [Keyboard Shortcuts Index](keyboard-shortcuts-index.md) for the complete list.

## Building the Documentation Site

This documentation can be built as a searchable website using MkDocs:

```bash
# Install dependencies
pip install -r requirements.txt

# Serve locally
mkdocs serve

# Build static site
mkdocs build

# Deploy to GitHub Pages
mkdocs gh-deploy
```

## Usage

Clone this repository or browse individual files:

```bash
# Clone the docs
git clone https://github.com/your-username/docs.git

# Open a cheatsheet
cat docs/omakub/fzf-cheatsheet.md

# Or use your editor
nvim docs/

# Or serve as website
cd docs && mkdocs serve
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
- [Docker](https://docs.docker.com/) - Container platform
- [tmux](https://github.com/tmux/tmux/wiki) - Terminal multiplexer

### Learning Resources
- [Vim Adventures](https://vim-adventures.com/) - Learn Vim through games
- [Learn Git Branching](https://learngitbranching.js.org/) - Interactive Git tutorial
- [Vimtutor](https://vimschool.netlify.app/introduction/vimtutor/) - Built-in Vim tutorial

## License

This documentation is provided as-is for educational purposes.

---

**Happy coding!**
