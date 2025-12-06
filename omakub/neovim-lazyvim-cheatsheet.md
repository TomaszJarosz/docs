# Neovim + LazyVim Cheatsheet

LazyVim is a modern, fully configured Neovim distribution with many plugins.

**Leader key:** `Space` (spacebar)

## Vim/Neovim Basics

### Modes
| Mode | Shortcut | Description |
|------|-------|------|
| Normal | `Esc` | Default mode, navigation and commands |
| Insert | `i`, `a`, `o` | Text editing mode |
| Visual | `v`, `V`, `Ctrl+v` | Text selection |
| Command | `:` | Execute commands |

### Basic Navigation (Normal Mode)

**Basics:**
| Shortcut | Action |
|-------|-------|
| `h/j/k/l` | Left/Down/Up/Right |
| `w` | Next word |
| `b` | Previous word |
| `e` | End of word |
| `0` | Beginning of line |
| `^` | First character in line |
| `$` | End of line |
| `gg` | Beginning of file |
| `G` | End of file |
| `{` / `}` | Previous/next paragraph |
| `Ctrl+d` | Half page down |
| `Ctrl+u` | Half page up |
| `Ctrl+f` | Page down |
| `Ctrl+b` | Page up |

**Search:**
| Shortcut | Action |
|-------|-------|
| `/text` | Search forward |
| `?text` | Search backward |
| `n` | Next match |
| `N` | Previous match |
| `*` | Search word under cursor |
| `#` | Search word under cursor (backward) |

### Editing (Normal Mode)

**Entering Insert Mode:**
| Shortcut | Action |
|-------|-------|
| `i` | Insert before cursor |
| `a` | Insert after cursor |
| `I` | Insert at beginning of line |
| `A` | Insert at end of line |
| `o` | New line below |
| `O` | New line above |

**Deleting:**
| Shortcut | Action |
|-------|-------|
| `x` | Delete character |
| `dd` | Delete line |
| `dw` | Delete word |
| `d$` | Delete to end of line |
| `d0` | Delete to beginning of line |
| `D` | Delete to end of line (like d$) |

**Copying and Pasting:**
| Shortcut | Action |
|-------|-------|
| `yy` | Copy line |
| `yw` | Copy word |
| `y$` | Copy to end of line |
| `p` | Paste after cursor |
| `P` | Paste before cursor |

**Change (Change = Delete + Insert):**
| Shortcut | Action |
|-------|-------|
| `cc` | Change line |
| `cw` | Change word |
| `c$` | Change to end of line |
| `C` | Change to end of line (like c$) |

**Other:**
| Shortcut | Action |
|-------|-------|
| `u` | Undo |
| `Ctrl+r` | Redo |
| `.` | Repeat last action |
| `~` | Toggle case |
| `>>` | Indent right |
| `<<` | Indent left |
| `==` | Auto-format line |

### Visual Mode

| Shortcut | Action |
|-------|-------|
| `v` | Visual mode (character by character) |
| `V` | Visual line mode (line by line) |
| `Ctrl+v` | Visual block mode (block) |
| `o` | Go to other end of selection |
| `d` | Delete selection |
| `y` | Copy selection |
| `c` | Change selection |
| `>` | Indent right |
| `<` | Indent left |
| `=` | Auto-format |

## LazyVim Specific

### Leader Menu (`Space`)

After pressing `Space`, a menu with hints appears (which-key).

### Files and Buffers

| Shortcut | Action |
|-------|-------|
| `<leader>ff` | Find Files (telescope) |
| `<leader>fr` | Recent Files |
| `<leader>fg` | Grep in files |
| `<leader>fb` | Find Buffers |
| `<leader>fn` | New file |
| `<leader>e` | File Explorer (neo-tree) |
| `<leader>E` | File Explorer (buffer) |

### Buffers and Windows

| Shortcut | Action |
|-------|-------|
| `<leader>bd` | Delete buffer |
| `<leader>bo` | Delete other buffers |
| `[b` | Previous buffer |
| `]b` | Next buffer |
| `<leader>bb` | Switch to previous buffer |
| `Ctrl+h/j/k/l` | Navigate between windows |
| `<leader>w` | Window management menu |
| `<leader>wd` | Close window |
| `<leader>-` | Split horizontal |
| `<leader>\|` | Split vertical |

### Code Navigation

| Shortcut | Action |
|-------|-------|
| `gd` | Go to Definition |
| `gr` | Go to References |
| `gI` | Go to Implementation |
| `gy` | Go to Type Definition |
| `K` | Hover Documentation |
| `gK` | Signature Help |
| `[d` | Previous diagnostic |
| `]d` | Next diagnostic |
| `<leader>cd` | Line Diagnostics |
| `<leader>ca` | Code Action |
| `<leader>cr` | Rename |

### LSP (Language Server Protocol)

| Shortcut | Action |
|-------|-------|
| `<leader>cl` | LSP Info |
| `<leader>cf` | Format Document |
| `<leader>cs` | Symbols (Outline) |

### Search / Replace

| Shortcut | Action |
|-------|-------|
| `<leader>sg` | Grep (Live grep) |
| `<leader>sw` | Grep word under cursor |
| `<leader>ss` | Buffer local search |
| `<leader>sR` | Search & Replace in files |
| `<leader>/` | Grep in open buffers |

### Git

| Shortcut | Action |
|-------|-------|
| `<leader>gg` | Lazygit (if installed) |
| `<leader>gb` | Git Blame Line |
| `<leader>gB` | Git Browse |
| `]h` | Next git hunk |
| `[h` | Previous git hunk |
| `<leader>ghp` | Preview hunk |
| `<leader>ghr` | Reset hunk |
| `<leader>ghs` | Stage hunk |

### Terminal

| Shortcut | Action |
|-------|-------|
| `<leader>ft` | Terminal (root dir) |
| `<leader>fT` | Terminal (cwd) |
| `<C-/>` | Toggle terminal (in terminal) |
| `<Esc><Esc>` | Exit terminal mode |

### Tabs

| Shortcut | Action |
|-------|-------|
| `<leader><tab>l` | List tabs |
| `<leader><tab><tab>` | New tab |
| `<leader><tab>d` | Close tab |
| `<leader><tab>n` | Next tab |
| `<leader><tab>p` | Previous tab |

### Telescope (Fuzzy Finder)

In Telescope:
| Shortcut | Action |
|-------|-------|
| `Ctrl+j/k` | Up/Down |
| `Ctrl+u/d` | Preview scroll |
| `Enter` | Open |
| `Ctrl+x` | Open in split |
| `Ctrl+v` | Open in vsplit |
| `Ctrl+t` | Open in new tab |
| `Ctrl+/` | Help |

### Neo-tree (File Explorer)

| Shortcut | Action |
|-------|-------|
| `<leader>e` | Toggle explorer |
| `<leader>E` | Explorer (current buffer) |

In Neo-tree:
| Shortcut | Action |
|-------|-------|
| `a` | Add file/folder |
| `d` | Delete |
| `r` | Rename |
| `y` | Copy to clipboard |
| `x` | Cut to clipboard |
| `p` | Paste |
| `c` | Copy file |
| `m` | Move file |
| `q` | Close |
| `?` | Help |

### Misc LazyVim

| Shortcut | Action |
|-------|-------|
| `<leader>l` | Lazy (plugin manager) |
| `<leader>xl` | Location list |
| `<leader>xq` | Quickfix list |
| `<leader>uf` | Toggle auto format (on save) |
| `<leader>ul` | Toggle line numbers |
| `<leader>ur` | Toggle relative line numbers |
| `<leader>uw` | Toggle word wrap |
| `<leader>L` | LazyVim changelog |
| `<leader>n` | Notifications |
| `<leader>qq` | Quit all |

### Comments

| Shortcut | Action |
|-------|-------|
| `gcc` | Toggle line comment |
| `gbc` | Toggle block comment |
| `gc` (visual) | Toggle comment on selection |

## Tips & Tricks

### 1. Which-Key
Press `Space` and wait - a menu with all available shortcuts will appear!

### 2. Telescope for everything
- `<leader>ff` - find files
- `<leader>sg` - search in content
- `<leader>sh` - help tags
- `<leader>sk` - keymaps
- `<leader>sc` - commands

### 3. LSP Auto-completion
In insert mode:
- `Ctrl+Space` - trigger completion
- `Ctrl+n/p` - next/previous suggestion
- `Enter` - accept
- `Ctrl+e` - close

### 4. Multi-cursor (Visual Block)
1. `Ctrl+v` - visual block mode
2. Select column
3. `I` - insert at beginning of all lines
4. `A` - insert at end of all lines

### 5. Text Objects
Super powerful! Format: `<action><a/i><object>`
- `ciw` - change inner word
- `ci"` - change inside quotes
- `di(` - delete inside parentheses
- `ya{` - yank around braces
- `vi[` - visual inside brackets

### 6. Macros
1. `q<letter>` - start recording macro
2. Perform actions
3. `q` - stop recording
4. `@<letter>` - play macro
5. `@@` - repeat last macro

### 7. Marks (Bookmarks)
- `m<letter>` - set mark
- `'<letter>` - jump to mark
- `''` - jump to previous position

### 8. Registers (Clipboards)
- `"<letter>y` - copy to register
- `"<letter>p` - paste from register
- `"+y` - copy to system clipboard
- `"+p` - paste from system clipboard

## Commands (Command Mode)

Press `:` in normal mode:

| Command | Action |
|---------|-------|
| `:w` | Save |
| `:q` | Quit |
| `:wq` or `:x` | Save and quit |
| `:q!` | Quit without saving |
| `:e file` | Open file |
| `:bn` / `:bp` | Next/Previous buffer |
| `:bd` | Delete buffer |
| `:%s/old/new/g` | Replace in entire file |
| `:10,20s/old/new/g` | Replace in lines 10-20 |
| `:set nu` | Show line numbers |
| `:set rnu` | Relative line numbers |
| `:help <topic>` | Help |

## LazyVim Extras

LazyVim has many "extras" (additional plugins). Check:
- `:LazyExtras` - list of available extras
- Select what you want to enable (e.g., language support)

## Common Issues

### LSP not working
```
:LspInfo
```
Check if language server is installed. Install via:
```
:Mason
```

### Plugin not working
```
:Lazy
```
Update plugins: `U`

### Reset configuration
```bash
# Backup
mv ~/.config/nvim ~/.config/nvim.backup
mv ~/.local/share/nvim ~/.local/share/nvim.backup

# Fresh start
git clone https://github.com/LazyVim/starter ~/.config/nvim
```

## Resources

- LazyVim Docs: https://www.lazyvim.org/
- Vim Cheatsheet: https://vim.rtorr.com/
- Interactive Tutorial: run `vimtutor` in terminal

---

**Quick start:**
1. Open file: `nvim file.txt`
2. `i` - insert mode
3. Type...
4. `Esc` - normal mode
5. `:w` - save
6. `Space` - see LazyVim menu
7. `:q` - quit

**Remember:**
- `Esc` - always returns to normal mode
- `Space` - leader key, opens menu
- `u` - undo
- `:w` - save
- `:q` - quit
