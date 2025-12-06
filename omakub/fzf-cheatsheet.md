# fzf - Fuzzy Finder Cheatsheet

fzf to potężny fuzzy finder dla command line - pozwala szybko wyszukiwać pliki, komendy, procesy i wiele więcej.

## Podstawy

### Instalacja i Konfiguracja (Omakub)

W Omakub fzf jest już zainstalowany i skonfigurowany!

**Sprawdź wersję:**
```bash
fzf --version
```

**Konfiguracja (opcjonalna):**
Dodaj do `~/.bashrc`:
```bash
# fzf theme
export FZF_DEFAULT_OPTS="--height 40% --layout=reverse --border --inline-info"

# Używaj ripgrep zamiast find
export FZF_DEFAULT_COMMAND='rg --files --hidden --follow --glob "!.git/*"'

# Dla Ctrl+T
export FZF_CTRL_T_COMMAND="$FZF_DEFAULT_COMMAND"

# Dla Alt+C
export FZF_ALT_C_COMMAND='fd --type d --hidden --follow --exclude .git'
```

## Wbudowane Skróty Klawiszowe

Omakub konfiguruje te skróty automatycznie:

### Ctrl+T - Fuzzy File Search

```bash
# Naciśnij Ctrl+T w command line
vim <Ctrl+T>
# Pojawi się interaktywny finder
# Wybierz plik(i) i naciśnij Enter
# Ścieżka zostanie wklejona do command line
```

**Przykłady:**
```bash
vim <Ctrl+T>              # Otwórz plik w vim
cat <Ctrl+T>              # Wyświetl plik
code <Ctrl+T>             # Otwórz w VSCode
rm <Ctrl+T>               # Usuń plik (ostrożnie!)
```

### Ctrl+R - Command History Search

```bash
# Naciśnij Ctrl+R
# Wpisz część komendy
# Fuzzy search w historii
# Enter aby wykonać lub Tab aby edytować
```

Znacznie lepsze niż domyślne Ctrl+R w bash!

### Alt+C - Directory Jump

```bash
# Naciśnij Alt+C
# Fuzzy search katalogów
# Enter aby CD do wybranego
```

**Tip:** Połącz z `z` lub `zoxide` dla super szybkiej nawigacji!

## Nawigacja w fzf

Kiedy fzf jest otwarty:

| Skrót | Akcja |
|-------|-------|
| `↑/↓` lub `Ctrl+k/j` | Góra/dół |
| `Ctrl+u/d` | Page up/down |
| `Tab` | Zaznacz/odznacz (multi-select) |
| `Shift+Tab` | Odznacz/zaznacz |
| `Ctrl+a` | Zaznacz wszystko |
| `Ctrl+d` | Odznacz wszystko |
| `Enter` | Akceptuj wybór |
| `Esc` lub `Ctrl+c` | Anuluj |
| `Ctrl+/` | Toggle preview window |
| `Shift+↑/↓` | Scroll preview |
| `?` | Toggle preview |

## Podstawowe Użycie w CLI

### 1. Prosty Fuzzy Find

```bash
# Znajdź i wypisz plik
find * -type f | fzf

# Z ripgrep (szybsze)
rg --files | fzf

# Z fd (nowocześniejsze)
fd | fzf
```

### 2. Interaktywny Wybór

```bash
# Wybierz plik i otwórz w vim
vim $(fzf)

# Wybierz katalog i cd
cd $(find . -type d | fzf)

# Lepiej z fd:
cd $(fd -t d | fzf)
```

### 3. Preview Window

```bash
# Preview plików z bat
fzf --preview 'bat --color=always {}'

# Preview z numerami linii
fzf --preview 'bat -n --color=always {}'

# Preview katalogów
fzf --preview 'ls -la {}'

# Preview z tree
fzf --preview 'tree -C {}'
```

### 4. Multi-Select

```bash
# Zaznacz wiele plików (Tab)
vim $(fzf -m)

# Usuń wiele plików
rm $(fzf -m)

# Dodaj do git
git add $(fzf -m)
```

## Zaawansowane Użycie

### Filtrowanie i Opcje

```bash
# Dokładne dopasowanie (prefix ')
fzf -q "'exact"

# Dokładny suffix match ($)
fzf -q "txt$"

# Prefix match (^)
fzf -q "^src"

# Negacja (!)
fzf -q "!test"

# OR (|)
fzf -q "jpg$ | png$"

# AND (spacja)
fzf -q "src test"
```

**Query syntax:**
- `'exact` - exact match
- `^prefix` - prefix match
- `suffix$` - suffix match
- `!not` - negacja
- `term1 term2` - AND
- `term1 | term2` - OR

### Layout i Appearance

```bash
# Reverse layout (wyniki na górze)
fzf --reverse

# Z ramką
fzf --border

# Wysokość
fzf --height 40%
fzf --height 100%

# Pozycja
fzf --layout=reverse
fzf --layout=default

# Inline info
fzf --inline-info

# No mouse
fzf --no-mouse

# Multi-select
fzf -m
fzf --multi
```

## Przydatne Funkcje Bash

Dodaj do `~/.bashrc`:

### 1. Szybkie Otwieranie Plików

```bash
# fe - Fuzzy Edit (otwórz w edytorze)
fe() {
    local file
    file=$(fzf --preview 'bat --color=always {}') && nvim "$file"
}

# fcd - Fuzzy CD
fcd() {
    local dir
    dir=$(fd -t d | fzf --preview 'tree -C {} | head -100') && cd "$dir"
}

# fo - Fuzzy Open (xdg-open)
fo() {
    local file
    file=$(fzf --preview 'bat --color=always {}') && xdg-open "$file"
}
```

### 2. Git Integration

```bash
# fgb - Fuzzy Git Branch (checkout)
fgb() {
    git branch -a | grep -v HEAD | \
    fzf --preview 'git log --oneline --graph --date=short --pretty="format:%C(auto)%cd %h%d %s" $(sed "s/.* //" <<< {}) | head -50' | \
    sed "s/.* //" | sed "s#remotes/[^/]*/##" | \
    xargs git checkout
}

# fgs - Fuzzy Git Show (zobacz commit)
fgs() {
    git log --oneline --color=always | \
    fzf --ansi --preview 'git show --color=always {1}' | \
    cut -d ' ' -f 1 | xargs git show
}

# fga - Fuzzy Git Add
fga() {
    git status -s | \
    fzf -m --preview 'git diff --color=always {2}' | \
    awk '{print $2}' | xargs git add
}

# fgd - Fuzzy Git Diff
fgd() {
    git status -s | \
    fzf --preview 'git diff --color=always {2}'
}
```

### 3. Process Management

```bash
# fkill - Fuzzy Kill Process
fkill() {
    local pid
    pid=$(ps -ef | sed 1d | fzf -m | awk '{print $2}')
    if [ "x$pid" != "x" ]; then
        echo $pid | xargs kill -${1:-9}
    fi
}

# Usage: fkill lub fkill 15 (SIGTERM)
```

### 4. History Search Enhanced

```bash
# fh - Fuzzy History (lepsze niż Ctrl+R)
fh() {
    eval $(history | fzf --tac --no-sort | sed 's/ *[0-9]* *//')
}
```

### 5. Docker Integration

```bash
# fdi - Fuzzy Docker Image
fdi() {
    docker images | fzf --header-lines=1 | awk '{print $3}'
}

# fdc - Fuzzy Docker Container
fdc() {
    docker ps -a | fzf --header-lines=1 | awk '{print $1}'
}

# fdl - Fuzzy Docker Logs
fdl() {
    docker ps -a | fzf --header-lines=1 | awk '{print $1}' | xargs docker logs -f
}

# fdsh - Fuzzy Docker Shell
fdsh() {
    docker ps | fzf --header-lines=1 | awk '{print $1}' | xargs -I {} docker exec -it {} /bin/bash
}
```

### 6. Znajdź i Edytuj (Ripgrep Integration)

```bash
# frg - Fuzzy Ripgrep (szukaj w zawartości plików)
frg() {
    rg --color=always --line-number --no-heading --smart-case "${*:-}" |
    fzf --ansi \
        --color "hl:-1:underline,hl+:-1:underline:reverse" \
        --delimiter : \
        --preview 'bat --color=always {1} --highlight-line {2}' \
        --preview-window 'up,60%,border-bottom,+{2}+3/3,~3' \
        --bind 'enter:become(nvim {1} +{2})'
}

# Usage: frg "search term"
```

### 7. Man Pages

```bash
# fman - Fuzzy Man Pages
fman() {
    man -k . | fzf --preview 'man {1}' | awk '{print $1}' | xargs man
}
```

### 8. SSH Hosts

```bash
# fssh - Fuzzy SSH
fssh() {
    local host
    host=$(grep -E '^Host ' ~/.ssh/config | sed 's/Host //' | fzf)
    if [ -n "$host" ]; then
        ssh "$host"
    fi
}
```

## Integracja z Innymi Narzędziami

### Z Vim/Neovim

**Plugin: fzf.vim**
```vim
" W ~/.config/nvim/init.vim lub init.lua
Plug 'junegunn/fzf', { 'do': { -> fzf#install() } }
Plug 'junegunn/fzf.vim'

" Skróty:
nnoremap <C-p> :Files<CR>
nnoremap <C-f> :Rg<CR>
nnoremap <leader>b :Buffers<CR>
```

### Z Zellij/tmux

```bash
# W Zellij - fuzzy session switch
zellij list-sessions | fzf | xargs zellij attach

# Alias:
alias zs='zellij list-sessions | fzf | xargs zellij attach'
```

### Z bat (Better Cat)

```bash
# Preview z bat (syntax highlighting)
export FZF_CTRL_T_OPTS="--preview 'bat -n --color=always {}'"
export FZF_ALT_C_OPTS="--preview 'tree -C {} | head -100'"
```

### Z fd (Better Find)

```bash
# Użyj fd zamiast find
export FZF_DEFAULT_COMMAND='fd --type f --hidden --follow --exclude .git'
export FZF_CTRL_T_COMMAND="$FZF_DEFAULT_COMMAND"
export FZF_ALT_C_COMMAND='fd --type d --hidden --follow --exclude .git'
```

## Przykładowe Workflow

### 1. Deweloperski Workflow

```bash
# Szybko otwórz projekt
cd ~/projects
cd $(fd -t d | fzf)

# Znajdź i edytuj plik
vim $(fzf --preview 'bat --color=always {}')

# Szukaj w kodzie i edytuj
frg "function name"  # Otwiera nvim na właściwej linii

# Git commit z fzf
fga  # Fuzzy add files
gc "commit message"
```

### 2. System Administration

```bash
# Sprawdź procesy i zabij
fkill

# Zobacz logi
journalctl | fzf

# SSH do serwera
fssh
```

### 3. File Management

```bash
# Znajdź i usuń
rm $(fzf -m)

# Znajdź i skopiuj
cp $(fzf -m) /destination/

# Znajdź i przenieś
mv $(fzf -m) /destination/
```

## Konfiguracja Kolorów

Dodaj do `~/.bashrc`:

```bash
# fzf color scheme (Tokyo Night)
export FZF_DEFAULT_OPTS=$FZF_DEFAULT_OPTS'
  --color=fg:#c0caf5,bg:#1a1b26,hl:#ff9e64
  --color=fg+:#c0caf5,bg+:#292e42,hl+:#ff9e64
  --color=info:#7aa2f7,prompt:#7dcfff,pointer:#7dcfff
  --color=marker:#9ece6a,spinner:#9ece6a,header:#9ece6a'

# Lub Catppuccin:
export FZF_DEFAULT_OPTS=$FZF_DEFAULT_OPTS'
  --color=bg+:#313244,bg:#1e1e2e,spinner:#f5e0dc,hl:#f38ba8
  --color=fg:#cdd6f4,header:#f38ba8,info:#cba6f7,pointer:#f5e0dc
  --color=marker:#f5e0dc,fg+:#cdd6f4,prompt:#cba6f7,hl+:#f38ba8'
```

## Kompletny ~/.bashrc Setup

```bash
# fzf configuration
export FZF_DEFAULT_OPTS="
  --height 40%
  --layout=reverse
  --border
  --inline-info
  --preview-window=:hidden
  --bind '?:toggle-preview'
  --bind 'ctrl-/:toggle-preview'
  --bind 'ctrl-u:preview-page-up'
  --bind 'ctrl-d:preview-page-down'
"

# Używaj ripgrep
export FZF_DEFAULT_COMMAND='rg --files --hidden --follow --glob "!.git/*"'
export FZF_CTRL_T_COMMAND="$FZF_DEFAULT_COMMAND"
export FZF_ALT_C_COMMAND='fd --type d --hidden --follow --exclude .git'

# Preview
export FZF_CTRL_T_OPTS="--preview 'bat -n --color=always {}'"
export FZF_ALT_C_OPTS="--preview 'tree -C {} | head -100'"

# Funkcje (dodaj wszystkie z sekcji "Przydatne Funkcje Bash" powyżej)
fe() { ... }
fcd() { ... }
fgb() { ... }
# itd.
```

## Tips & Tricks

### 1. Exclude Patterns

```bash
# Ignoruj node_modules, .git, etc
rg --files --hidden --follow \
  -g '!{.git,node_modules,target,dist,build}/*' | fzf
```

### 2. Szybkie Aliasy

```bash
alias f='fzf'
alias ff='fzf --preview "bat --color=always {}"'
alias v='vim $(fzf)'
```

### 3. Pipe do fzf

```bash
# Wszystko można pipe'ować do fzf!
ls | fzf
history | fzf
docker ps | fzf
kubectl get pods | fzf
```

### 4. Custom Key Bindings

```bash
# W fzf możesz definiować własne akcje
fzf --bind 'ctrl-e:execute(nvim {})'
fzf --bind 'ctrl-y:execute-silent(echo {} | xclip)'
```

### 5. Multi-Stage Pipeline

```bash
# Wybierz katalog, potem plik w nim
cd $(fd -t d | fzf) && vim $(fzf)
```

## Performance Tips

1. **Użyj ripgrep/fd zamiast find** - znacznie szybsze
2. **Ogranicz głębokość** - `fd --max-depth 3`
3. **Exclude duże katalogi** - node_modules, .git, target
4. **Cache file list** dla dużych projektów:
```bash
# Generuj listę plików raz
fd > /tmp/files.txt
cat /tmp/files.txt | fzf
```

## Troubleshooting

### fzf nie znajduje plików

```bash
# Sprawdź FZF_DEFAULT_COMMAND
echo $FZF_DEFAULT_COMMAND

# Reset do domyślnego
unset FZF_DEFAULT_COMMAND
```

### Skróty nie działają

```bash
# Upewnij się że fzf key bindings są załadowane
# Powinno być w ~/.bashrc:
[ -f ~/.fzf.bash ] && source ~/.fzf.bash
```

### Preview nie działa

```bash
# Zainstaluj bat
sudo apt install bat
# lub
cargo install bat

# Zainstaluj tree
sudo apt install tree
```

## Zasoby

- **fzf GitHub:** https://github.com/junegunn/fzf
- **fzf Wiki:** https://github.com/junegunn/fzf/wiki
- **Advanced Examples:** https://github.com/junegunn/fzf/wiki/examples
- `man fzf` - Dokumentacja
- **Interactive Tutorial:** po prostu zacznij używać Ctrl+T/Ctrl+R!

## Szybki Start

```bash
# Wypróbuj wbudowane:
Ctrl+T     # Fuzzy file search
Ctrl+R     # Fuzzy command history
Alt+C      # Fuzzy directory jump

# Podstawowe użycie:
vim $(fzf)
cd $(fd -t d | fzf)
kill $(ps -ef | fzf | awk '{print $2}')

# Z preview:
fzf --preview 'bat --color=always {}'
```

**Zapamiętaj:**
- Wszystko może być input dla fzf (pipe)
- Tab = multi-select
- ? = toggle preview
- fzf + bat + ripgrep + fd = super combo!
