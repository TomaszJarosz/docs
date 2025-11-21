# Neovim + LazyVim Cheatsheet

LazyVim to nowoczesna, w pełni skonfigurowana dystrybucja Neovim z wieloma pluginami.

**Leader key:** `Space` (spacja)

## Podstawy Vim/Neovim

### Tryby
| Tryb | Skrót | Opis |
|------|-------|------|
| Normal | `Esc` | Domyślny tryb, poruszanie i komendy |
| Insert | `i`, `a`, `o` | Tryb edycji tekstu |
| Visual | `v`, `V`, `Ctrl+v` | Zaznaczanie tekstu |
| Command | `:` | Wykonywanie komend |

### Podstawowe Poruszanie (Normal Mode)

**Podstawy:**
| Skrót | Akcja |
|-------|-------|
| `h/j/k/l` | Lewo/Dół/Góra/Prawo |
| `w` | Następne słowo |
| `b` | Poprzednie słowo |
| `e` | Koniec słowa |
| `0` | Początek linii |
| `^` | Pierwszy znak w linii |
| `$` | Koniec linii |
| `gg` | Początek pliku |
| `G` | Koniec pliku |
| `{` / `}` | Poprzedni/następny paragraf |
| `Ctrl+d` | Pół strony w dół |
| `Ctrl+u` | Pół strony w górę |
| `Ctrl+f` | Strona w dół |
| `Ctrl+b` | Strona w górę |

**Wyszukiwanie:**
| Skrót | Akcja |
|-------|-------|
| `/tekst` | Szukaj do przodu |
| `?tekst` | Szukaj wstecz |
| `n` | Następne dopasowanie |
| `N` | Poprzednie dopasowanie |
| `*` | Szukaj słowa pod kursorem |
| `#` | Szukaj słowa pod kursorem (wstecz) |

### Edycja (Normal Mode)

**Wchodzenie w Insert Mode:**
| Skrót | Akcja |
|-------|-------|
| `i` | Insert przed kursorem |
| `a` | Insert za kursorem |
| `I` | Insert na początku linii |
| `A` | Insert na końcu linii |
| `o` | Nowa linia poniżej |
| `O` | Nowa linia powyżej |

**Usuwanie:**
| Skrót | Akcja |
|-------|-------|
| `x` | Usuń znak |
| `dd` | Usuń linię |
| `dw` | Usuń słowo |
| `d$` | Usuń do końca linii |
| `d0` | Usuń do początku linii |
| `D` | Usuń do końca linii (jak d$) |

**Kopiowanie i Wklejanie:**
| Skrót | Akcja |
|-------|-------|
| `yy` | Kopiuj linię |
| `yw` | Kopiuj słowo |
| `y$` | Kopiuj do końca linii |
| `p` | Wklej za kursorem |
| `P` | Wklej przed kursorem |

**Zmiana (Change = Delete + Insert):**
| Skrót | Akcja |
|-------|-------|
| `cc` | Zmień linię |
| `cw` | Zmień słowo |
| `c$` | Zmień do końca linii |
| `C` | Zmień do końca linii (jak c$) |

**Inne:**
| Skrót | Akcja |
|-------|-------|
| `u` | Cofnij (undo) |
| `Ctrl+r` | Ponów (redo) |
| `.` | Powtórz ostatnią akcję |
| `~` | Zmień wielkość litery |
| `>>` | Wcięcie w prawo |
| `<<` | Wcięcie w lewo |
| `==` | Auto-formatuj linię |

### Visual Mode

| Skrót | Akcja |
|-------|-------|
| `v` | Visual mode (znak po znaku) |
| `V` | Visual line mode (linia po linii) |
| `Ctrl+v` | Visual block mode (blok) |
| `o` | Przejdź do drugiego końca zaznaczenia |
| `d` | Usuń zaznaczenie |
| `y` | Kopiuj zaznaczenie |
| `c` | Zmień zaznaczenie |
| `>` | Wcięcie w prawo |
| `<` | Wcięcie w lewo |
| `=` | Auto-formatuj |

## LazyVim Specific

### Leader Menu (`Space`)

Po naciśnięciu `Space` pojawia się menu z podpowiedziami (which-key).

### Pliki i Bufory

| Skrót | Akcja |
|-------|-------|
| `<leader>ff` | Find Files (telescope) |
| `<leader>fr` | Recent Files |
| `<leader>fg` | Grep w plikach |
| `<leader>fb` | Find Buffers |
| `<leader>fn` | Nowy plik |
| `<leader>e` | File Explorer (neo-tree) |
| `<leader>E` | File Explorer (buffer) |

### Bufory i Okna

| Skrót | Akcja |
|-------|-------|
| `<leader>bd` | Delete buffer |
| `<leader>bo` | Delete other buffers |
| `[b` | Poprzedni bufor |
| `]b` | Następny bufor |
| `<leader>bb` | Przełącz na poprzedni bufor |
| `Ctrl+h/j/k/l` | Nawigacja między oknami |
| `<leader>w` | Menu zarządzania oknami |
| `<leader>wd` | Zamknij okno |
| `<leader>-` | Split horizontal |
| `<leader>\|` | Split vertical |

### Code Navigation

| Skrót | Akcja |
|-------|-------|
| `gd` | Go to Definition |
| `gr` | Go to References |
| `gI` | Go to Implementation |
| `gy` | Go to Type Definition |
| `K` | Hover Documentation |
| `gK` | Signature Help |
| `[d` | Poprzedni diagnostic |
| `]d` | Następny diagnostic |
| `<leader>cd` | Line Diagnostics |
| `<leader>ca` | Code Action |
| `<leader>cr` | Rename |

### LSP (Language Server Protocol)

| Skrót | Akcja |
|-------|-------|
| `<leader>cl` | LSP Info |
| `<leader>cf` | Format Document |
| `<leader>cs` | Symbols (Outline) |

### Search / Replace

| Skrót | Akcja |
|-------|-------|
| `<leader>sg` | Grep (Live grep) |
| `<leader>sw` | Grep słowa pod kursorem |
| `<leader>ss` | Buffer local search |
| `<leader>sR` | Search & Replace w plikach |
| `<leader>/` | Grep w otwartych buforach |

### Git

| Skrót | Akcja |
|-------|-------|
| `<leader>gg` | Lazygit (jeśli zainstalowane) |
| `<leader>gb` | Git Blame Line |
| `<leader>gB` | Git Browse |
| `]h` | Następny git hunk |
| `[h` | Poprzedni git hunk |
| `<leader>ghp` | Preview hunk |
| `<leader>ghr` | Reset hunk |
| `<leader>ghs` | Stage hunk |

### Terminal

| Skrót | Akcja |
|-------|-------|
| `<leader>ft` | Terminal (root dir) |
| `<leader>fT` | Terminal (cwd) |
| `<C-/>` | Toggle terminal (w terminalu) |
| `<Esc><Esc>` | Wyjdź z terminal mode |

### Tabs

| Skrót | Akcja |
|-------|-------|
| `<leader><tab>l` | Lista tabów |
| `<leader><tab><tab>` | Nowy tab |
| `<leader><tab>d` | Zamknij tab |
| `<leader><tab>n` | Następny tab |
| `<leader><tab>p` | Poprzedni tab |

### Telescope (Fuzzy Finder)

W Telescope:
| Skrót | Akcja |
|-------|-------|
| `Ctrl+j/k` | Góra/Dół |
| `Ctrl+u/d` | Preview scroll |
| `Enter` | Otwórz |
| `Ctrl+x` | Otwórz w split |
| `Ctrl+v` | Otwórz w vsplit |
| `Ctrl+t` | Otwórz w nowym tabie |
| `Ctrl+/` | Pomoc |

### Neo-tree (File Explorer)

| Skrót | Akcja |
|-------|-------|
| `<leader>e` | Toggle explorer |
| `<leader>E` | Explorer (current buffer) |

W Neo-tree:
| Skrót | Akcja |
|-------|-------|
| `a` | Add file/folder |
| `d` | Delete |
| `r` | Rename |
| `y` | Copy to clipboard |
| `x` | Cut to clipboard |
| `p` | Paste |
| `c` | Copy file |
| `m` | Move file |
| `q` | Zamknij |
| `?` | Pomoc |

### Misc LazyVim

| Skrót | Akcja |
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

| Skrót | Akcja |
|-------|-------|
| `gcc` | Toggle line comment |
| `gbc` | Toggle block comment |
| `gc` (visual) | Toggle comment na zaznaczeniu |

## Tips & Tricks

### 1. Which-Key
Naciśnij `Space` i poczekaj - pojawi się menu z wszystkimi dostępnymi skrótami!

### 2. Telescope dla wszystkiego
- `<leader>ff` - szukaj plików
- `<leader>sg` - szukaj w zawartości
- `<leader>sh` - help tags
- `<leader>sk` - keymaps
- `<leader>sc` - commands

### 3. LSP Auto-completion
W insert mode:
- `Ctrl+Space` - trigger completion
- `Ctrl+n/p` - następna/poprzednia sugestia
- `Enter` - akceptuj
- `Ctrl+e` - zamknij

### 4. Multi-cursor (Visual Block)
1. `Ctrl+v` - visual block mode
2. Zaznacz kolumnę
3. `I` - insert na początku wszystkich linii
4. `A` - insert na końcu wszystkich linii

### 5. Text Objects
Super potężne! Format: `<akcja><a/i><obiekt>`
- `ciw` - change inner word
- `ci"` - change inside quotes
- `di(` - delete inside parentheses
- `ya{` - yank around braces
- `vi[` - visual inside brackets

### 6. Makra
1. `q<litera>` - zacznij nagrywać makro
2. Wykonaj akcje
3. `q` - zakończ nagrywanie
4. `@<litera>` - odtwórz makro
5. `@@` - powtórz ostatnie makro

### 7. Marks (Zakładki)
- `m<litera>` - ustaw mark
- `'<litera>` - skocz do marka
- `''` - skocz do poprzedniej pozycji

### 8. Registers (Schowki)
- `"<litera>y` - kopiuj do rejestru
- `"<litera>p` - wklej z rejestru
- `"+y` - kopiuj do schowka systemowego
- `"+p` - wklej ze schowka systemowego

## Komendy (Command Mode)

Naciśnij `:` w normal mode:

| Komenda | Akcja |
|---------|-------|
| `:w` | Zapisz |
| `:q` | Wyjdź |
| `:wq` lub `:x` | Zapisz i wyjdź |
| `:q!` | Wyjdź bez zapisywania |
| `:e plik` | Otwórz plik |
| `:bn` / `:bp` | Next/Previous buffer |
| `:bd` | Delete buffer |
| `:%s/old/new/g` | Replace w całym pliku |
| `:10,20s/old/new/g` | Replace w liniach 10-20 |
| `:set nu` | Pokaż numery linii |
| `:set rnu` | Relative line numbers |
| `:help <temat>` | Pomoc |

## LazyVim Extras

LazyVim ma wiele "extras" (dodatkowe pluginy). Sprawdź:
- `:LazyExtras` - lista dostępnych extras
- Wybierz co chcesz włączyć (np. support dla języków)

## Najczęstsze Problemy

### LSP nie działa
```
:LspInfo
```
Sprawdź czy language server jest zainstalowany. Zainstaluj przez:
```
:Mason
```

### Plugin nie działa
```
:Lazy
```
Zaktualizuj pluginy: `U`

### Resetuj konfigurację
```bash
# Backup
mv ~/.config/nvim ~/.config/nvim.backup
mv ~/.local/share/nvim ~/.local/share/nvim.backup

# Fresh start
git clone https://github.com/LazyVim/starter ~/.config/nvim
```

## Zasoby

- LazyVim Docs: https://www.lazyvim.org/
- Vim Cheatsheet: https://vim.rtorr.com/
- Interactive Tutorial: uruchom `vimtutor` w terminalu

---

**Szybki start:**
1. Otwórz plik: `nvim plik.txt`
2. `i` - insert mode
3. Pisz...
4. `Esc` - normal mode
5. `:w` - zapisz
6. `Space` - zobacz menu LazyVim
7. `:q` - wyjdź

**Zapamiętaj:**
- `Esc` - zawsze wraca do normal mode
- `Space` - leader key, otwiera menu
- `u` - undo
- `:w` - save
- `:q` - quit
