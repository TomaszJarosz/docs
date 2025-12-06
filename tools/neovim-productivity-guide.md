# Neovim - Productivity Guide for Programmers

Comprehensive Neovim guide for programmers who want to achieve maximum productivity.

## Vim/Neovim Philosophy

**Modal Editing** - different modes for different tasks:
- **Normal Mode** - navigation and commands (default)
- **Insert Mode** - writing text
- **Visual Mode** - selection
- **Command Mode** - executing commands

**Goal:** Spend most time in Normal Mode, brief visits to Insert Mode

**Thinking:** Not "move cursor and type", but "execute operation"

## Basic Modes

### Mode Switching

| Key | From → To | Description |
|---------|--------|------|
| `Esc` | Any → Normal | **ALWAYS returns to Normal** |
| `i` | Normal → Insert | Insert before cursor |
| `a` | Normal → Insert | Insert after cursor (append) |
| `I` | Normal → Insert | Insert at beginning of line |
| `A` | Normal → Insert | Insert at end of line |
| `o` | Normal → Insert | New line below |
| `O` | Normal → Insert | New line above |
| `v` | Normal → Visual | Visual mode (char) |
| `V` | Normal → Visual Line | Visual mode (line) |
| `Ctrl+v` | Normal → Visual Block | Visual mode (block) |
| `:` | Normal → Command | Command mode |

**Golden rule:** `Esc` always returns to Normal Mode!

## Navigation (Normal Mode)

### Basic Movements

```
      ↑ k
← h       l →
    ↓ j

h - left
j - down
k - up
l - right
```

**Don't use arrows!** Your fingers never leave the home row.

### Word Movements

| Key | Action |
|---------|-------|
| `w` | Next word (beginning) |
| `W` | Next WORD (ignore punctuation) |
| `e` | End of word |
| `E` | End of WORD |
| `b` | Previous word |
| `B` | Previous WORD |
| `ge` | End of previous word |

**Word vs WORD:**
- `word` - word (separated by special characters)
- `WORD` - string (separated only by space)

Example: `user.getName()` has 5 words but 1 WORD

### Line Movements

| Key | Action |
|---------|-------|
| `0` | Beginning of line (column 0) |
| `^` | First character (non-whitespace) |
| `$` | End of line |
| `g_` | Last character (non-whitespace) |
| `f{char}` | Find char (forward) |
| `F{char}` | Find char (backward) |
| `t{char}` | Till char (forward) |
| `T{char}` | Till char (backward) |
| `;` | Repeat last f/F/t/T |
| `,` | Repeat last f/F/t/T (reverse) |

**Example:**
```
cursor here: int getUserName() {
             ^
f(  → int getUserName() {
                      ^
```

### File Movements

| Key | Action |
|---------|-------|
| `gg` | Beginning of file |
| `G` | End of file |
| `{number}G` | Go to line {number} |
| `{number}gg` | Go to line {number} |
| `%` | Go to matching bracket |
| `{` | Previous paragraph |
| `}` | Next paragraph |
| `[[` | Previous section/function |
| `]]` | Next section/function |

### Screen Movements

| Key | Action |
|---------|-------|
| `Ctrl+d` | Half page down |
| `Ctrl+u` | Half page up |
| `Ctrl+f` | Full page down (forward) |
| `Ctrl+b` | Full page up (backward) |
| `H` | Top of screen (High) |
| `M` | Middle of screen |
| `L` | Bottom of screen (Low) |
| `zt` | Scroll - cursor at top |
| `zz` | Scroll - cursor in middle |
| `zb` | Scroll - cursor at bottom |

## Editing (Normal Mode)

### Operators

Vim uses **operators** + **motion**:

**Format:** `operator + motion`

**Main operators:**
- `d` - delete (cut)
- `c` - change (delete + insert mode)
- `y` - yank (copy)
- `v` - visual select

**Examples:**
- `dw` - delete word
- `d$` - delete to end of line
- `cw` - change word (delete and enter insert)
- `yy` - yank line (copy)

### Deleting (Delete)

| Key | Action |
|---------|-------|
| `x` | Delete char under cursor |
| `X` | Delete char before cursor |
| `dd` | Delete line |
| `D` | Delete to end of line (like `d$`) |
| `dw` | Delete word |
| `diw` | Delete inner word |
| `daw` | Delete a word (with space) |
| `di"` | Delete inside quotes |
| `da"` | Delete around quotes (with quotes) |
| `di(` | Delete inside parentheses |
| `da(` | Delete around parentheses |
| `dG` | Delete to end of file |
| `dgg` | Delete to beginning of file |

### Changing (Change = Delete + Insert)

| Key | Action |
|---------|-------|
| `cc` | Change line |
| `C` | Change to end of line |
| `cw` | Change word |
| `ciw` | Change inner word |
| `ci"` | Change inside quotes |
| `ci{` | Change inside braces |
| `ct;` | Change till semicolon |

### Copying and Pasting (Yank & Put)

| Key | Action |
|---------|-------|
| `yy` | Yank (copy) line |
| `Y` | Yank line (like `yy`) |
| `yw` | Yank word |
| `yiw` | Yank inner word |
| `y$` | Yank to end of line |
| `p` | Put (paste) after cursor/below |
| `P` | Put before cursor/above |
| `gp` | Put and move cursor after pasted text |

### Undo & Redo

| Key | Action |
|---------|-------|
| `u` | Undo |
| `Ctrl+r` | Redo |
| `U` | Undo all changes on line |

### Repeating

| Key | Action |
|---------|-------|
| `.` | **Repeat last change** (SUPER IMPORTANT!) |
| `@:` | Repeat last command |

**Example `.` (dot command):**
```
1. ciw → change word to "user"
2. n → find next occurrence
3. . → repeat change (automatically changes to "user")
4. n, . → next one
```

## Text Objects - Vim's Greatest Power

**Format:** `operator + i/a + object`

- `i` - **inner** (inside, without delimiters)
- `a` - **around** (with, with delimiters)

### Available Objects

| Object | Description |
|--------|------|
| `w` | word |
| `W` | WORD |
| `s` | sentence |
| `p` | paragraph |
| `"` | double quotes |
| `'` | single quotes |
| `` ` `` | backticks |
| `(` or `)` | parentheses |
| `{` or `}` | braces |
| `[` or `]` | brackets |
| `<` or `>` | angle brackets |
| `t` | tag (HTML/XML) |

### Examples

```javascript
function getUserName(user) {
    return user.name;
}
```

**Cursor on `user` inside function:**
- `ciw` → change inner word → change "user"
- `ci(` → change inside parentheses → change parameter
- `ci{` → change inside braces → change entire function body
- `da{` → delete around braces → delete entire function

**Cursor anywhere in string:**
```javascript
const message = "Hello, World!";
```
- `ci"` → change inside quotes → change string content
- `da"` → delete around quotes → delete entire string with quotes

**HTML:**
```html
<div class="container">Content here</div>
```
- `cit` → change inside tag → change "Content here"
- `cat` → change around tag → change `<div...>Content here</div>`
- `dat` → delete around tag → delete entire `<div>...</div>`

## Searching

### Basic Search

| Key | Action |
|---------|-------|
| `/pattern` | Search forward |
| `?pattern` | Search backward |
| `n` | Next match |
| `N` | Previous match |
| `*` | Search word under cursor (forward) |
| `#` | Search word under cursor (backward) |
| `g*` | Partial match forward |
| `g#` | Partial match backward |

### Search with Replace

```vim
:%s/old/new/g          " Replace in entire file
:%s/old/new/gc         " Replace with confirmation
:s/old/new/g           " Replace in line
:'<,'>s/old/new/g      " Replace in selection (visual)
```

**Flags:**
- `g` - global (all in line)
- `c` - confirm (ask for each)
- `i` - case insensitive

## Visual Mode

### Visual Modes

| Key | Mode |
|---------|------|
| `v` | Character-wise |
| `V` | Line-wise |
| `Ctrl+v` | Block-wise |
| `gv` | Re-select last visual selection |

### Operations in Visual Mode

After selection:
- `d` - delete
- `c` - change
- `y` - yank
- `>` - indent right
- `<` - indent left
- `=` - auto-indent
- `~` - toggle case
- `u` - lowercase
- `U` - uppercase

### Visual Block (Column)

**Super power for programmers!**

```
1. Ctrl+v → start block selection
2. j/k → select multiple lines
3. I → insert before block
4. Type text
5. Esc → text appears in all lines!
```

**Example - add comment:**
```javascript
// Before:
const a = 1;
const b = 2;
const c = 3;

// Ctrl+v, jj, I, //, Esc
// After:
// const a = 1;
// const b = 2;
// const c = 3;
```

## Macros - Automation

### Recording and Playback

```
1. q{letter} → start recording macro to register {letter}
2. ... perform operations ...
3. q → stop recording
4. @{letter} → play macro
5. @@ → repeat last macro
6. {number}@{letter} → execute macro {number} times
```

**Example:**

```javascript
// You have:
getUserId
getUserName
getUserEmail

// You want:
const userId = getUserId();
const userName = getUserName();
const userEmail = getUserEmail();

// Macro:
1. qa              → start recording to 'a'
2. Iconst <Esc>    → add "const "
3. A();<Esc>       → add "();"
4. j               → next line
5. q               → stop

6. 2@a             → execute 2 times on remaining lines
```

## Counts and Repetitions

**Format:** `{count} + {operator/motion}`

**Examples:**
- `3j` - 3 lines down
- `5w` - 5 words forward
- `2dd` - delete 2 lines
- `3cw` - change 3 words
- `10p` - paste 10 times
- `100i-<Esc>` - insert 100 dashes

## Indentation and Formatting

| Key | Action |
|---------|-------|
| `>>` | Indent line right |
| `<<` | Indent line left |
| `==` | Auto-indent line |
| `>%` | Indent block (on bracket) |
| `=%` | Auto-indent block |
| `gg=G` | Auto-indent entire file |
| `gq` | Format text (wrap) |

**Visual mode:**
```
V → select lines
> → indent
```

## Registers

Vim has multiple clipboards (registers):

### Main Registers

| Register | Description |
|---------|------|
| `"` | Unnamed (default) |
| `0` | Last yank |
| `1-9` | Delete history |
| `a-z` | Named registers (user) |
| `+` | System clipboard |
| `*` | Selection clipboard |
| `%` | Filename |
| `/` | Last search |
| `:` | Last command |

### Usage

```vim
"ayy        " Yank line to register 'a'
"ap         " Paste from register 'a'
"+y         " Yank to system clipboard
"+p         " Paste from system clipboard
:reg        " View register contents
```

## Marks

Bookmarks in file/files:

```vim
m{letter}       " Set mark
'{letter}       " Jump to mark (beginning of line)
`{letter}       " Jump to mark (exact position)
:marks          " List marks

" Usage:
ma              " Set mark 'a'
... do something elsewhere ...
'a              " Return to mark 'a'
```

**Lowercase letters (a-z):** local (in file)
**Uppercase letters (A-Z):** global (between files)

## Practical Workflows

### Scenario 1: Refactor Variable Name

```
1. * → find all occurrences
2. cgn → change next match
3. Type new name
4. Esc
5. . → repeat on next (n + .)
6. . . . → next ones
```

**Alternative:**
```
:%s/oldName/newName/gc
```

### Scenario 2: Add Logging

```javascript
function processUser(user) {
    // Want to add console.log before return
    return user.id;
}

// Workflow:
1. /return<Enter>  → find return
2. O               → new line above
3. console.log('user:', user);
4. Esc
5. n               → next return
6. .               → repeat (O + text)
```

### Scenario 3: Change String to Template Literal

```javascript
// Before:
const msg = "Hello " + name + "!";

// After:
const msg = `Hello ${name}!`;

// Workflow:
1. f" → jump to first "
2. r` → replace with `
3. f+ → jump to +
4. 3s${<Esc> → replace " + with ${
5. f+ → second +
6. 2s}<Esc> → replace + " with }
7. f" → last "
8. r` → replace with `
```

### Scenario 4: Multi-line Edit (Block)

```javascript
// Add export before each function:
function getUserId() {}
function getUserName() {}
function getUserEmail() {}

// Workflow:
1. Ctrl+v → block visual
2. 2j → select 3 lines
3. I → insert mode
4. export <Esc>
5. Done!

export function getUserId() {}
export function getUserName() {}
export function getUserEmail() {}
```

### Scenario 5: Sort & Unique Lines

```vim
" Select lines in Visual mode (V)
:sort           " Sort
:sort u         " Sort and remove duplicates

" Or entire file:
:%sort
:%sort u
```

### Scenario 6: Copy Method to Another Class

```
1. va{ → select entire method (visual around braces)
2. y → yank
3. :e OtherClass.java → open other file
4. /class<Enter> → find class
5. } → go to first method
6. P → paste above
```

## Command Mode - Powerful Commands

### Basic

```vim
:w              " Write (save)
:q              " Quit
:wq or :x       " Write and quit
:q!             " Quit without saving
:e filename     " Edit file
:bn             " Next buffer
:bp             " Previous buffer
:bd             " Delete buffer
:ls             " List buffers
:help topic     " Help
```

### Advanced

```vim
:!command       " Execute shell command
:r !command     " Read output of command into buffer
:%!jq           " Filter entire buffer through jq
:'<,'>!sort     " Sort selected lines

" Examples:
:!ls            " View files
:r !date        " Insert date
:%!python -m json.tool  " Format JSON
```

### Range Operations

```vim
:10,20d         " Delete lines 10-20
:10,20y         " Yank lines 10-20
:10,20s/old/new/g   " Replace in lines 10-20
:.,$d           " Delete from current to end
:%d             " Delete everything (% = entire file)
:'<,'>          " Visual selection (auto-added)
```

## Splits & Tabs

### Splits (Windows)

```vim
:split file     " Horizontal split
:vsplit file    " Vertical split
Ctrl+w s        " Horizontal split
Ctrl+w v        " Vertical split
Ctrl+w q        " Close split
Ctrl+w h/j/k/l  " Navigate splits
Ctrl+w H/J/K/L  " Move split
Ctrl+w =        " Equal size
Ctrl+w _        " Maximize height
Ctrl+w |        " Maximize width
```

### Tabs

```vim
:tabnew file    " New tab
:tabn           " Next tab
:tabp           " Previous tab
:tabclose       " Close tab
gt              " Next tab
gT              " Previous tab
{n}gt           " Go to tab n
```

## Must-Have Plugins

### LSP (Language Server Protocol)

```vim
" In LazyVim already configured:
gd              " Go to definition
gr              " References
K               " Hover documentation
<leader>ca      " Code actions
<leader>rn      " Rename
]d              " Next diagnostic
[d              " Previous diagnostic
```

### Telescope / Fuzzy Finder

```vim
<leader>ff      " Find files
<leader>fg      " Find in files (grep)
<leader>fb      " Find buffers
<leader>fh      " Find help
<leader>fo      " Find old files
```

### File Explorer

```vim
<leader>e       " Toggle file explorer
```

### Git Integration

```vim
<leader>gg      " Git status (LazyGit)
]c              " Next change (hunk)
[c              " Previous change
<leader>hp      " Preview hunk
<leader>hs      " Stage hunk
<leader>hu      " Unstage hunk
```

## Vimrc - Essential Settings

```vim
" ~/.config/nvim/init.vim or init.lua

" Basic
set number              " Line numbers
set relativenumber      " Relative line numbers
set mouse=a             " Mouse support
set clipboard=unnamedplus  " System clipboard

" Tabs and indentation
set tabstop=4           " Tab = 4 spaces
set shiftwidth=4        " Indent = 4 spaces
set expandtab           " Spaces instead of tabs
set autoindent          " Auto indent
set smartindent         " Smart indent

" Search
set ignorecase          " Case insensitive search
set smartcase           " Case sensitive if uppercase
set incsearch           " Incremental search
set hlsearch            " Highlight search

" UI
set cursorline          " Highlight current line
set signcolumn=yes      " Always show sign column
set scrolloff=8         " Keep 8 lines above/below cursor
set wrap                " Wrap lines
set linebreak           " Wrap at word boundaries

" Performance
set updatetime=300      " Faster completion
set timeoutlen=500      " Faster key sequence

" Split
set splitright          " Vertical split right
set splitbelow          " Horizontal split below
```

## Remaps - Productivity Boost

```vim
" Leader key
let mapleader = " "

" Better navigation
nnoremap <C-d> <C-d>zz     " Keep cursor centered
nnoremap <C-u> <C-u>zz
nnoremap n nzzzv
nnoremap N Nzzzv

" Move lines
vnoremap J :m '>+1<CR>gv=gv    " Move line down
vnoremap K :m '<-2<CR>gv=gv    " Move line up

" Better paste
vnoremap p "_dP            " Paste without copying

" Quick save
nnoremap <leader>w :w<CR>

" Quick quit
nnoremap <leader>q :q<CR>

" Split navigation
nnoremap <C-h> <C-w>h
nnoremap <C-j> <C-w>j
nnoremap <C-k> <C-w>k
nnoremap <C-l> <C-w>l

" Buffer navigation
nnoremap <Tab> :bn<CR>
nnoremap <S-Tab> :bp<CR>

" Clear search highlight
nnoremap <Esc> :noh<CR>

" Better indenting
vnoremap < <gv
vnoremap > >gv

" Replace word under cursor
nnoremap <leader>r :%s/\<<C-r><C-w>\>//g<Left><Left>
```

## Tips & Tricks

### 1. Ciw > dw

```
Instead of: dw (delete word - but cursor must be at beginning)
Use: ciw (change inner word - works anywhere in word)
```

### 2. Dot Command Optimization

```
Always think: "Will I repeat this?"
If yes - use . (dot)

Example:
Instead of: ciw → type → Esc → w → ciw → type → Esc
Use: ciw → type → Esc → w → . → w → .
```

### 3. Relative Line Numbers

```
:set relativenumber

Now you can: 5j (instead of jjjjj)
             3k (instead of kkk)
```

### 4. Search and Change

```
/pattern<Enter>  → find
cgn → change next match
. . . → repeat on next ones

Faster than :%s/old/new/g for few changes!
```

### 5. Case Conversion

```
~ → toggle case (on character)
gU{motion} → uppercase (e.g. gUiw - uppercase word)
gu{motion} → lowercase
```

### 6. Join Lines

```
J → join next line (remove newline)
gJ → join without adding space
```

### 7. Auto-completion (Insert Mode)

```
Ctrl+n → Next completion
Ctrl+p → Previous completion
Ctrl+x Ctrl+f → File path completion
Ctrl+x Ctrl+l → Line completion
```

### 8. Ex Commands Range

```
:g/pattern/d → delete all lines with pattern
:g!/pattern/d → delete all lines WITHOUT pattern
:v/pattern/d → same as above
```

## Keyboard-Only Challenge

Complete without mouse:

1. ✅ Open file (Neovim + filename)
2. ✅ Find function (/<name>)
3. ✅ Copy function (va{y)
4. ✅ Go to end of file (G)
5. ✅ Paste (p)
6. ✅ Change function name (ciw)
7. ✅ Add comment above (O)
8. ✅ Auto-indent (==)
9. ✅ Save (:w)
10. ✅ Quit (:q)

**If you used mouse - repeat!**

## Learning Path

### Week 1: Basics
```
Day 1-2: Movements (hjkl, w, b, 0, $)
Day 3-4: Modes (i, a, o, v, Esc)
Day 5: Operators (d, c, y) + motion
Day 6-7: Text objects (iw, i", i()
```

### Week 2: Workflow
```
Day 1-2: Dot command (.)
Day 3-4: Searching (/, *, n)
Day 5: Visual mode & blocks
Day 6-7: Registers & clipboard
```

### Week 3: Mastery
```
Day 1-2: Macros (q)
Day 3-4: Splits & buffers
Day 5: Advanced motions
Day 6-7: Custom mappings
```

### Week 4: Speed
```
- Use only keyboard
- Goal: 80% operations without thinking
- Master . (dot) command
- Use vimtutor (vim -c 'Tutor')
```

## Vimtutor

**Best way to learn!**

```bash
# Run tutorial
nvim -c 'Tutor'

# Or in Neovim:
:Tutor

# 30 minutes daily for a week = mastered basics
```

## Useful Commands

### Statistics

```vim
g Ctrl+g        " Word count, line count
```

### Spell Check

```vim
:set spell spelllang=en_us
]s              " Next misspelled
[s              " Previous misspelled
z=              " Suggestions
zg              " Add to dictionary
```

### Diff Mode

```vim
:vert diffsplit file2   " Diff with file2
]c                      " Next change
[c                      " Previous change
do                      " Diff obtain (get change)
dp                      " Diff put (send change)
```

## Resources

- `:help user-manual` - official documentation
- `:Tutor` - interactive tutorial
- https://vim-adventures.com/ - game for learning Vim
- https://vimgolf.com/ - Vim challenges
- https://github.com/ThePrimeagen/vim-be-good - practice plugin

## Mindset

**Instead of:** Move cursor and edit
**Think:** What operation + on what (operator + text object)

**Instead of:** Mouse and arrows
**Think:** hjkl and w/b/e

**Instead of:** "How to do this?"
**Think:** "How to do this repeatably?" (. command)

**Goal:**
- Week 1: Frustration (this is normal!)
- Week 2: Understanding
- Week 3: Fluency
- Month: Can't imagine another editor

---

## Quick Reference Card

```
MOVEMENT:
hjkl    left/down/up/right      w/b     word forward/back
0/$     start/end line          gg/G    start/end file
%       matching bracket        f{char} find char

EDIT:
i/a     insert before/after     o/O     new line below/above
dd      delete line             yy      yank line
p/P     paste after/before      u       undo
.       repeat last change      Ctrl+r  redo

OPERATORS + TEXT OBJECTS:
ciw     change inner word       di(     delete inside ()
ca"     change around "         vi{     visual inside {}
daw     delete a word           ya(     yank around ()

VISUAL:
v       char visual             V       line visual
Ctrl+v  block visual            gv      reselect

SEARCH:
/text   search forward          n/N     next/prev
*/#     search word under       :%s/old/new/g  replace

COMMAND:
:w      save                    :q      quit
:e file open file               :bn/:bp next/prev buffer
```

🚀 **Keep your fingers on home row, keep your mind in flow!**
