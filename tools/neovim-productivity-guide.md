# Neovim - Productivity Guide dla Programisty

Kompleksowy przewodnik po Neovim dla programistów, którzy chcą osiągnąć maksymalną produktywność.

## Filozofia Vim/Neovim

**Modal Editing** - różne tryby do różnych zadań:
- **Normal Mode** - nawigacja i komendy (domyślny)
- **Insert Mode** - pisanie tekstu
- **Visual Mode** - zaznaczanie
- **Command Mode** - wykonywanie komend

**Cel:** Większość czasu w Normal Mode, krótkie wizyty w Insert Mode

**Myślenie:** Nie "przesuń kursor i wpisz", ale "wykonaj operację"

## Podstawowe Tryby

### Przełączanie Trybów

| Klawisz | Z → Do | Opis |
|---------|--------|------|
| `Esc` | Any → Normal | **ZAWSZE wraca do Normal** |
| `i` | Normal → Insert | Insert przed kursorem |
| `a` | Normal → Insert | Insert za kursorem (append) |
| `I` | Normal → Insert | Insert na początku linii |
| `A` | Normal → Insert | Insert na końcu linii |
| `o` | Normal → Insert | Nowa linia poniżej |
| `O` | Normal → Insert | Nowa linia powyżej |
| `v` | Normal → Visual | Visual mode (char) |
| `V` | Normal → Visual Line | Visual mode (line) |
| `Ctrl+v` | Normal → Visual Block | Visual mode (block) |
| `:` | Normal → Command | Command mode |

**Złota zasada:** `Esc` zawsze wraca do Normal Mode!

## Nawigacja (Normal Mode)

### Podstawowe Ruchy

```
      ↑ k
← h       l →
    ↓ j

h - lewo
j - dół
k - góra
l - prawo
```

**Nie używaj strzałek!** Twoje palce nie opuszczają home row.

### Ruchy po Słowach

| Klawisz | Akcja |
|---------|-------|
| `w` | Next word (początek) |
| `W` | Next WORD (ignore punctuation) |
| `e` | End of word |
| `E` | End of WORD |
| `b` | Previous word |
| `B` | Previous WORD |
| `ge` | End of previous word |

**Word vs WORD:**
- `word` - słowo (rozdzielane przez znaki specjalne)
- `WORD` - ciąg znaków (rozdzielany tylko spacją)

Przykład: `user.getName()` ma 5 words ale 1 WORD

### Ruchy po Linii

| Klawisz | Akcja |
|---------|-------|
| `0` | Początek linii (kolumna 0) |
| `^` | Pierwszy znak (nie-whitespace) |
| `$` | Koniec linii |
| `g_` | Ostatni znak (nie-whitespace) |
| `f{char}` | Find char (forward) |
| `F{char}` | Find char (backward) |
| `t{char}` | Till char (forward) |
| `T{char}` | Till char (backward) |
| `;` | Repeat last f/F/t/T |
| `,` | Repeat last f/F/t/T (reverse) |

**Przykład:**
```
cursor here: int getUserName() {
             ^
f(  → int getUserName() {
                      ^
```

### Ruchy po Pliku

| Klawisz | Akcja |
|---------|-------|
| `gg` | Początek pliku |
| `G` | Koniec pliku |
| `{number}G` | Idź do linii {number} |
| `{number}gg` | Idź do linii {number} |
| `%` | Idź do matchującego nawiasu/bracketu |
| `{` | Poprzedni paragraf |
| `}` | Następny paragraf |
| `[[` | Poprzednia sekcja/funkcja |
| `]]` | Następna sekcja/funkcja |

### Ruchy po Ekranie

| Klawisz | Akcja |
|---------|-------|
| `Ctrl+d` | Pół strony w dół |
| `Ctrl+u` | Pół strony w górę |
| `Ctrl+f` | Pełna strona w dół (forward) |
| `Ctrl+b` | Pełna strona w górę (backward) |
| `H` | Top of screen (High) |
| `M` | Middle of screen |
| `L` | Bottom of screen (Low) |
| `zt` | Scroll - kursor na górze |
| `zz` | Scroll - kursor w środku |
| `zb` | Scroll - kursor na dole |

## Edycja (Normal Mode)

### Operatory

Vim używa **operatorów** + **motion**:

**Format:** `operator + motion`

**Główne operatory:**
- `d` - delete (cut)
- `c` - change (delete + insert mode)
- `y` - yank (copy)
- `v` - visual select

**Przykłady:**
- `dw` - delete word
- `d$` - delete do końca linii
- `cw` - change word (usuń i wejdź w insert)
- `yy` - yank line (copy)

### Usuwanie (Delete)

| Klawisz | Akcja |
|---------|-------|
| `x` | Delete char pod kursorem |
| `X` | Delete char przed kursorem |
| `dd` | Delete line |
| `D` | Delete do końca linii (jak `d$`) |
| `dw` | Delete word |
| `diw` | Delete inner word |
| `daw` | Delete a word (with space) |
| `di"` | Delete inside quotes |
| `da"` | Delete around quotes (with quotes) |
| `di(` | Delete inside parentheses |
| `da(` | Delete around parentheses |
| `dG` | Delete do końca pliku |
| `dgg` | Delete do początku pliku |

### Zmiana (Change = Delete + Insert)

| Klawisz | Akcja |
|---------|-------|
| `cc` | Change line |
| `C` | Change do końca linii |
| `cw` | Change word |
| `ciw` | Change inner word |
| `ci"` | Change inside quotes |
| `ci{` | Change inside braces |
| `ct;` | Change till semicolon |

### Kopiowanie i Wklejanie (Yank & Put)

| Klawisz | Akcja |
|---------|-------|
| `yy` | Yank (copy) line |
| `Y` | Yank line (jak `yy`) |
| `yw` | Yank word |
| `yiw` | Yank inner word |
| `y$` | Yank do końca linii |
| `p` | Put (paste) za kursorem/poniżej |
| `P` | Put przed kursorem/powyżej |
| `gp` | Put i przesuń kursor za wklejony tekst |

### Undo & Redo

| Klawisz | Akcja |
|---------|-------|
| `u` | Undo |
| `Ctrl+r` | Redo |
| `U` | Undo all changes on line |

### Powtarzanie

| Klawisz | Akcja |
|---------|-------|
| `.` | **Powtórz ostatnią zmianę** (SUPER WAŻNE!) |
| `@:` | Powtórz ostatnią komendę |

**Przykład `.` (dot command):**
```
1. ciw → zmień słowo na "user"
2. n → znajdź następne wystąpienie
3. . → powtórz zmianę (automatycznie zmieni na "user")
4. n, . → kolejne
```

## Text Objects - Największa Moc Vim

**Format:** `operator + i/a + object`

- `i` - **inner** (inside, bez ograniczników)
- `a` - **around** (with, z ogranicznikami)

### Dostępne Obiekty

| Object | Opis |
|--------|------|
| `w` | word |
| `W` | WORD |
| `s` | sentence |
| `p` | paragraph |
| `"` | double quotes |
| `'` | single quotes |
| `` ` `` | backticks |
| `(` lub `)` | parentheses |
| `{` lub `}` | braces |
| `[` lub `]` | brackets |
| `<` lub `>` | angle brackets |
| `t` | tag (HTML/XML) |

### Przykłady

```javascript
function getUserName(user) {
    return user.name;
}
```

**Kursor na `user` w środku funkcji:**
- `ciw` → change inner word → zmień "user"
- `ci(` → change inside parentheses → zmień parametr
- `ci{` → change inside braces → zmień całe wnętrze funkcji
- `da{` → delete around braces → usuń całą funkcję

**Kursor gdziekolwiek w stringu:**
```javascript
const message = "Hello, World!";
```
- `ci"` → change inside quotes → zmień zawartość stringa
- `da"` → delete around quotes → usuń cały string z quotes

**HTML:**
```html
<div class="container">Content here</div>
```
- `cit` → change inside tag → zmień "Content here"
- `cat` → change around tag → zmień `<div...>Content here</div>`
- `dat` → delete around tag → usuń całe `<div>...</div>`

## Wyszukiwanie

### Podstawowe Wyszukiwanie

| Klawisz | Akcja |
|---------|-------|
| `/pattern` | Szukaj do przodu |
| `?pattern` | Szukaj wstecz |
| `n` | Next match |
| `N` | Previous match |
| `*` | Szukaj słowa pod kursorem (forward) |
| `#` | Szukaj słowa pod kursorem (backward) |
| `g*` | Partial match forward |
| `g#` | Partial match backward |

### Wyszukiwanie z Replace

```vim
:%s/old/new/g          " Replace w całym pliku
:%s/old/new/gc         " Replace z potwierdzeniem
:s/old/new/g           " Replace w linii
:'<,'>s/old/new/g      " Replace w zaznaczeniu (visual)
```

**Flagi:**
- `g` - global (wszystkie w linii)
- `c` - confirm (pytaj o każdą)
- `i` - case insensitive

## Visual Mode

### Tryby Visual

| Klawisz | Tryb |
|---------|------|
| `v` | Character-wise |
| `V` | Line-wise |
| `Ctrl+v` | Block-wise |
| `gv` | Re-select last visual selection |

### Operacje w Visual Mode

Po zaznaczeniu:
- `d` - delete
- `c` - change
- `y` - yank
- `>` - indent right
- `<` - indent left
- `=` - auto-indent
- `~` - toggle case
- `u` - lowercase
- `U` - uppercase

### Visual Block (Kolumnowy)

**Super power dla programistów!**

```
1. Ctrl+v → rozpocznij block selection
2. j/k → zaznacz wiele linii
3. I → insert przed blokiem
4. Wpisz tekst
5. Esc → tekst pojawi się we wszystkich liniach!
```

**Przykład - dodaj komentarz:**
```javascript
// Przed:
const a = 1;
const b = 2;
const c = 3;

// Ctrl+v, jj, I, //, Esc
// Po:
// const a = 1;
// const b = 2;
// const c = 3;
```

## Makra - Automatyzacja

### Nagrywanie i Odtwarzanie

```
1. q{letter} → rozpocznij nagrywanie makra do rejestru {letter}
2. ... wykonaj operacje ...
3. q → zakończ nagrywanie
4. @{letter} → odtwórz makro
5. @@ → powtórz ostatnie makro
6. {number}@{letter} → wykonaj makro {number} razy
```

**Przykład:**

```javascript
// Masz:
getUserId
getUserName
getUserEmail

// Chcesz:
const userId = getUserId();
const userName = getUserName();
const userEmail = getUserEmail();

// Makro:
1. qa              → rozpocznij nagrywanie do 'a'
2. Iconst <Esc>    → dodaj "const "
3. A();<Esc>       → dodaj "();"
4. j               → następna linia
5. q               → zakończ

6. 2@a             → wykonaj 2 razy na pozostałych liniach
```

## Liczniki i Powtórzenia

**Format:** `{count} + {operator/motion}`

**Przykłady:**
- `3j` - 3 linie w dół
- `5w` - 5 słów do przodu
- `2dd` - usuń 2 linie
- `3cw` - zmień 3 słowa
- `10p` - wklej 10 razy
- `100i-<Esc>` - wstaw 100 myślników

## Wcięcia i Formatowanie

| Klawisz | Akcja |
|---------|-------|
| `>>` | Indent line right |
| `<<` | Indent line left |
| `==` | Auto-indent line |
| `>%` | Indent block (na nawiasie) |
| `=%` | Auto-indent block |
| `gg=G` | Auto-indent cały plik |
| `gq` | Format text (wrap) |

**Visual mode:**
```
V → zaznacz linie
> → indent
```

## Rejestry (Registers)

Vim ma wiele schowków (rejestrów):

### Główne Rejestry

| Rejestr | Opis |
|---------|------|
| `"` | Unnamed (domyślny) |
| `0` | Ostatnie yank |
| `1-9` | Historia delete |
| `a-z` | Named registers (użytkownika) |
| `+` | System clipboard |
| `*` | Selection clipboard |
| `%` | Nazwa pliku |
| `/` | Ostatnie wyszukiwanie |
| `:` | Ostatnia komenda |

### Użycie

```vim
"ayy        " Yank line do rejestru 'a'
"ap         " Paste z rejestru 'a'
"+y         " Yank do system clipboard
"+p         " Paste ze system clipboard
:reg        " Zobacz zawartość rejestrów
```

## Marki (Marks)

Zakładki w pliku/plikach:

```vim
m{letter}       " Ustaw mark
'{letter}       " Skocz do mark (początek linii)
`{letter}       " Skocz do mark (exact position)
:marks          " Lista marks

" Użycie:
ma              " Ustaw mark 'a'
... zrób coś gdzie indziej ...
'a              " Wróć do mark 'a'
```

**Małe litery (a-z):** lokalne (w pliku)
**Duże litery (A-Z):** globalne (między plikami)

## Praktyczne Workflow

### Scenariusz 1: Refactor Nazwy Zmiennej

```
1. * → znajdź wszystkie wystąpienia
2. cgn → change next match
3. Wpisz nową nazwę
4. Esc
5. . → powtórz na następnym (n + .)
6. . . . → kolejne
```

**Alternatywa:**
```
:%s/oldName/newName/gc
```

### Scenariusz 2: Dodaj Logging

```javascript
function processUser(user) {
    // Chcesz dodać console.log przed return
    return user.id;
}

// Workflow:
1. /return<Enter>  → znajdź return
2. O               → nowa linia powyżej
3. console.log('user:', user);
4. Esc
5. n               → następny return
6. .               → powtórz (O + tekst)
```

### Scenariusz 3: Zmień String na Template Literal

```javascript
// Przed:
const msg = "Hello " + name + "!";

// Po:
const msg = `Hello ${name}!`;

// Workflow:
1. f" → skocz do pierwszego "
2. r` → zamień na `
3. f+ → skocz do +
4. 3s${<Esc> → zamień " + na ${
5. f+ → drugi +
6. 2s}<Esc> → zamień + " na }
7. f" → ostatni "
8. r` → zamień na `
```

### Scenariusz 4: Multi-line Edit (Block)

```javascript
// Dodaj export przed każdą funkcją:
function getUserId() {}
function getUserName() {}
function getUserEmail() {}

// Workflow:
1. Ctrl+v → block visual
2. 2j → zaznacz 3 linie
3. I → insert mode
4. export <Esc>
5. Gotowe!

export function getUserId() {}
export function getUserName() {}
export function getUserEmail() {}
```

### Scenariusz 5: Sort & Unique Lines

```vim
" Zaznacz linie w Visual mode (V)
:sort           " Sortuj
:sort u         " Sortuj i usuń duplikaty

" Lub całe file:
:%sort
:%sort u
```

### Scenariusz 6: Skopiuj Metodę do Innej Klasy

```
1. va{ → zaznacz całą metodę (visual around braces)
2. y → yank
3. :e OtherClass.java → otwórz inny plik
4. /class<Enter> → znajdź class
5. } → idź do pierwszej metody
6. P → paste powyżej
```

## Command Mode - Potężne Komendy

### Podstawowe

```vim
:w              " Write (save)
:q              " Quit
:wq lub :x      " Write and quit
:q!             " Quit without saving
:e filename     " Edit file
:bn             " Next buffer
:bp             " Previous buffer
:bd             " Delete buffer
:ls             " List buffers
:help topic     " Help
```

### Zaawansowane

```vim
:!command       " Wykonaj shell command
:r !command     " Read output of command into buffer
:%!jq           " Filter całego buffera przez jq
:'<,'>!sort     " Sort zaznaczonych linii

" Przykłady:
:!ls            " Zobacz pliki
:r !date        " Wstaw datę
:%!python -m json.tool  " Format JSON
```

### Range Operations

```vim
:10,20d         " Delete linie 10-20
:10,20y         " Yank linie 10-20
:10,20s/old/new/g   " Replace w liniach 10-20
:.,$d           " Delete od bieżącej do końca
:%d             " Delete wszystko (% = cały plik)
:'<,'>          " Visual selection (auto-dodane)
```

## Splits & Tabs

### Splits (Okna)

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

## Plugins Must-Have

### LSP (Language Server Protocol)

```vim
" W LazyVim już skonfigurowane:
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
" ~/.config/nvim/init.vim lub init.lua

" Podstawowe
set number              " Numery linii
set relativenumber      " Relative line numbers
set mouse=a             " Mouse support
set clipboard=unnamedplus  " System clipboard

" Taby i wcięcia
set tabstop=4           " Tab = 4 spaces
set shiftwidth=4        " Indent = 4 spaces
set expandtab           " Spacje zamiast tabów
set autoindent          " Auto indent
set smartindent         " Smart indent

" Wyszukiwanie
set ignorecase          " Case insensitive search
set smartcase           " Case sensitive jeśli uppercase
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
vnoremap p "_dP            " Paste bez kopiowania

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
Zamiast: dw (delete word - ale kursor musi być na początku)
Używaj: ciw (change inner word - działa gdziekolwiek w słowie)
```

### 2. Dot Command Optimization

```
Zawsze myśl: "Czy będę to powtarzać?"
Jeśli tak - użyj . (dot)

Przykład:
Zamiast: ciw → type → Esc → w → ciw → type → Esc
Użyj: ciw → type → Esc → w → . → w → .
```

### 3. Relative Line Numbers

```
:set relativenumber

Teraz możesz: 5j (zamiast jjjjj)
               3k (zamiast kkk)
```

### 4. Wyszukiwanie i Zmiana

```
/pattern<Enter>  → znajdź
cgn → change next match
. . . → powtarzaj na kolejnych

Szybsze niż :%s/old/new/g dla kilku zmian!
```

### 5. Case Conversion

```
~ → toggle case (na znaku)
gU{motion} → uppercase (np. gUiw - uppercase word)
gu{motion} → lowercase
```

### 6. Join Lines

```
J → join następną linię (usuń newline)
gJ → join bez dodawania spacji
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
:g/pattern/d → usuń wszystkie linie z pattern
:g!/pattern/d → usuń wszystkie linie BEZ pattern
:v/pattern/d → to samo co powyżej
```

## Keyboard-Only Challenge

Wykonaj bez myszy:

1. ✅ Otwórz plik (Neovim + filename)
2. ✅ Znajdź funkcję (/<name>)
3. ✅ Skopiuj funkcję (va{y)
4. ✅ Idź do końca pliku (G)
5. ✅ Wklej (p)
6. ✅ Zmień nazwę funkcji (ciw)
7. ✅ Dodaj komentarz powyżej (O)
8. ✅ Auto-indent (==)
9. ✅ Zapisz (:w)
10. ✅ Wyjdź (:q)

**Jeśli użyłeś myszy - powtórz!**

## Learning Path

### Tydzień 1: Podstawy
```
Dzień 1-2: Ruchy (hjkl, w, b, 0, $)
Dzień 3-4: Tryby (i, a, o, v, Esc)
Dzień 5: Operatory (d, c, y) + motion
Dzień 6-7: Text objects (iw, i", i()
```

### Tydzień 2: Workflow
```
Dzień 1-2: Dot command (.)
Dzień 3-4: Wyszukiwanie (/, *, n)
Dzień 5: Visual mode & blocks
Dzień 6-7: Registers & clipboard
```

### Tydzień 3: Mastery
```
Dzień 1-2: Makra (q)
Dzień 3-4: Splits & buffers
Dzień 5: Advanced motions
Dzień 6-7: Custom mappings
```

### Tydzień 4: Speed
```
- Używaj tylko klawiatury
- Cel: 80% operacji bez myśli
- Opanuj . (dot) command
- Użyj vimtutor (vim -c 'Tutor')
```

## Vimtutor

**Najlepszy sposób nauki!**

```bash
# Uruchom tutorial
nvim -c 'Tutor'

# Lub w Neovim:
:Tutor

# 30 minut dziennie przez tydzień = opanowane podstawy
```

## Przydatne Komendy

### Statystyki

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

## Zasoby

- `:help user-manual` - oficjalna dokumentacja
- `:Tutor` - interaktywny tutorial
- https://vim-adventures.com/ - gra do nauki Vim
- https://vimgolf.com/ - wyzwania Vim
- https://github.com/ThePrimeagen/vim-be-good - plugin do ćwiczeń

## Mindset

**Zamiast:** Ruszać kursor i edytować
**Myśl:** Jaka operacja + na czym (operator + text object)

**Zamiast:** Myszy i strzałek
**Myśl:** hjkl i w/b/e

**Zamiast:** "Jak to zrobić?"
**Myśl:** "Jak zrobić to powtarzalnie?" (. command)

**Cel:**
- Tydzień 1: Frustracja (to normalne!)
- Tydzień 2: Zrozumienie
- Tydzień 3: Płynność
- Miesiąc: Nie wyobrażasz sobie innego edytora

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
