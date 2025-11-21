# Shell Productivity - Cheatsheet

Zaawansowane triki i skróty dla produktywnej pracy w bash/shell.

## Skróty Klawiszowe Bash

### Nawigacja po Linii

| Skrót | Akcja |
|-------|-------|
| `Ctrl+a` | Początek linii |
| `Ctrl+e` | Koniec linii |
| `Alt+f` | Słowo do przodu |
| `Alt+b` | Słowo wstecz |
| `Ctrl+xx` | Toggle między początkiem a obecną pozycją |

### Edycja

| Skrót | Akcja |
|-------|-------|
| `Ctrl+k` | Wytnij do końca linii |
| `Ctrl+u` | Wytnij do początku linii |
| `Alt+d` | Wytnij słowo do przodu |
| `Alt+Backspace` | Wytnij słowo wstecz |
| `Ctrl+w` | Wytnij słowo wstecz (do spacji) |
| `Ctrl+y` | Wklej ostatnio wycięte |
| `Alt+t` | Zamień miejscami ostatnie 2 słowa |
| `Ctrl+t` | Zamień miejscami ostatnie 2 znaki |
| `Alt+u` | Uppercase słowo |
| `Alt+l` | Lowercase słowo |
| `Alt+c` | Capitalize słowo |

### Historia Komend

| Skrót | Akcja |
|-------|-------|
| `Ctrl+r` | Szukaj w historii (fzf w Omakub!) |
| `Ctrl+s` | Szukaj do przodu (po Ctrl+r) |
| `Ctrl+p` | Poprzednia komenda |
| `Ctrl+n` | Następna komenda |
| `Alt+.` | Ostatni argument poprzedniej komendy |
| `Alt+Shift+.` | Pierwszy argument poprzedniej komendy |
| `!!` | Poprzednia komenda |
| `!$` | Ostatni argument |
| `!^` | Pierwszy argument |
| `!*` | Wszystkie argumenty |
| `!n` | Komenda numer n z historii |
| `!-n` | n-ta komenda od końca |
| `!string` | Ostatnia komenda zaczynająca się na string |
| `!?string` | Ostatnia komenda zawierająca string |

### Kontrola

| Skrót | Akcja |
|-------|-------|
| `Ctrl+l` | Wyczyść ekran (jak `clear`) |
| `Ctrl+c` | Przerwij komendę (SIGINT) |
| `Ctrl+d` | Exit shell / EOF |
| `Ctrl+z` | Zawieś proces (bg aby wznowić w tle) |
| `Ctrl+s` | Zatrzymaj output (scroll lock) |
| `Ctrl+q` | Wznów output |

### Tab Completion

| Skrót | Akcja |
|-------|-------|
| `Tab` | Autocomplete |
| `Tab Tab` | Pokaż wszystkie możliwości |
| `Alt+/` | Complete filename |
| `Alt+~` | Complete username |
| `Alt+$` | Complete variable |
| `Alt+@` | Complete hostname |
| `Alt+*` | Insert wszystkie completion |

## Historia Komend

### Podstawy

```bash
# Zobacz historię
history

# Ostatnie 10 komend
history 10

# Szukaj w historii
history | grep keyword

# Wyczyść historię
history -c

# Usuń konkretny wpis
history -d 123
```

### Ekspansja Historii

```bash
# Wykonaj ostatnią komendę
!!

# Wykonaj jako sudo
sudo !!

# Ostatni argument
ls /long/path/to/file
cd !$              # cd /long/path/to/file

# Wszystkie argumenty
command arg1 arg2 arg3
another !*         # another arg1 arg2 arg3

# Zmień w ostatniej komendzie
!!:s/old/new       # Zamień old na new
^old^new           # Krótsza forma

# Przykład:
vim /etc/config
^vim^cat           # Wykonuje: cat /etc/config
```

### Konfiguracja Historii

Dodaj do `~/.bashrc`:
```bash
# Rozmiar historii
export HISTSIZE=10000
export HISTFILESIZE=20000

# Ignoruj duplikaty i komendy zaczynające się od spacji
export HISTCONTROL=ignoreboth:erasedups

# Ignoruj konkretne komendy
export HISTIGNORE="ls:ll:cd:pwd:exit:clear"

# Timestamp w historii
export HISTTIMEFORMAT="%F %T "

# Append zamiast overwrite
shopt -s histappend

# Zapisuj od razu (dla wielu terminali)
PROMPT_COMMAND="history -a; $PROMPT_COMMAND"
```

## Brace Expansion

```bash
# Zakres
echo {1..10}              # 1 2 3 4 5 6 7 8 9 10
echo {a..z}               # a b c d ... z
echo {01..10}             # 01 02 03 ... 10

# Lista
echo {jpg,png,gif}        # jpg png gif
mkdir {src,dist,test}     # Tworzy 3 foldery

# Kombinacje
touch file{1..3}.{js,css}
# Tworzy: file1.js file1.css file2.js file2.css file3.js file3.css

# Nested
mkdir -p project/{src/{js,css},dist,test}

# Backup
cp file.txt{,.bak}        # cp file.txt file.txt.bak

# Zakres z inkrementem
echo {0..100..10}         # 0 10 20 30 ... 100
```

## Parameter Expansion

```bash
# Podstawy
echo $VAR
echo ${VAR}

# Długość
echo ${#VAR}

# Substring
VAR="Hello World"
echo ${VAR:0:5}           # Hello
echo ${VAR:6}             # World

# Zamiana
echo ${VAR/World/Bash}    # Hello Bash (pierwsza)
echo ${VAR//o/0}          # Hell0 W0rld (wszystkie)

# Remove pattern
FILE="path/to/file.txt"
echo ${FILE##*/}          # file.txt (remove longest match from start)
echo ${FILE#*/}           # to/file.txt (remove shortest match)
echo ${FILE%%/*}          # path (remove longest match from end)
echo ${FILE%/*}           # path/to (remove shortest match)

# Extension tricks
echo ${FILE%.*}           # path/to/file (remove extension)
echo ${FILE##*.}          # txt (get extension)

# Default values
echo ${VAR:-default}      # Use default if VAR unset
echo ${VAR:=default}      # Set and use default if VAR unset
echo ${VAR:?error}        # Error if VAR unset
echo ${VAR:+value}        # Use value if VAR is set

# Case modification
VAR="hello"
echo ${VAR^}              # Hello (first char uppercase)
echo ${VAR^^}             # HELLO (all uppercase)
echo ${VAR,}              # hello (first char lowercase)
echo ${VAR,,}             # hello (all lowercase)
```

## Command Substitution i Piping

### Command Substitution

```bash
# Modern syntax (preferowane)
$(command)

# Old syntax
`command`

# Przykłady:
echo "Today is $(date)"
files=$(ls | wc -l)
current_dir=$(pwd)

# Nested
echo "Files: $(echo $(ls | wc -l))"
```

### Piping & Redirection

```bash
# Podstawowe
command1 | command2       # Pipe output
command > file            # Redirect output (overwrite)
command >> file           # Append output
command < file            # Input from file
command 2> file           # Redirect stderr
command &> file           # Redirect stdout i stderr
command 2>&1              # Redirect stderr to stdout

# Przydatne kombinacje:
# Przekieruj stdout i stderr do różnych plików
command > stdout.log 2> stderr.log

# Przekieruj stderr do stdout i pipe
command 2>&1 | grep error

# Ignoruj output
command > /dev/null
command &> /dev/null

# Tee - zapisz i wyświetl
command | tee file.log
command | tee -a file.log  # Append

# Here document
cat << EOF
Multiple lines
of text
EOF

# Here string
grep "pattern" <<< "string to search"
```

## Przydatne Komendy

### Directory Navigation

```bash
# cd tricks
cd -                      # Poprzedni katalog
cd                        # Home directory
cd ~user                  # Home użytkownika
cd ../..                  # Dwa poziomy w górę

# pushd/popd/dirs
pushd /tmp               # Idź do /tmp i zapamiętaj
pushd /var               # Idź do /var
dirs -v                  # Pokaż stack
popd                     # Wróć do poprzedniego

# Aliasy w ~/.bashrc:
alias ..='cd ..'
alias ...='cd ../..'
alias ....='cd ../../..'
```

### Finding Files

```bash
# find
find . -name "*.txt"
find . -type f -name "*.js"
find . -mtime -7              # Modified w ostatnich 7 dniach
find . -size +10M             # Większe niż 10MB
find . -name "*.log" -delete  # Znajdź i usuń

# fd (nowocześniejsze, szybsze)
fd pattern
fd -e txt                     # Extension
fd -t f                       # Type file
fd -H                         # Include hidden
fd pattern -x rm              # Execute command

# locate (szybkie, ale wymaga updatedb)
locate filename
updatedb                      # Update database (sudo)
```

### Text Processing

```bash
# grep
grep pattern file
grep -r pattern dir          # Recursive
grep -i pattern file         # Case insensitive
grep -v pattern file         # Invert (nie zawiera)
grep -n pattern file         # Z numerami linii
grep -c pattern file         # Policz dopasowania
grep -A 3 pattern file       # 3 linie po
grep -B 3 pattern file       # 3 linie przed
grep -C 3 pattern file       # 3 linie przed i po

# ripgrep (rg - szybsze)
rg pattern
rg -i pattern                # Case insensitive
rg -t py pattern             # Tylko pliki Python
rg -l pattern                # Tylko nazwy plików

# awk
awk '{print $1}' file        # Pierwsza kolumna
awk -F: '{print $1}' file    # Custom delimiter
ps aux | awk '$3 > 50'       # Filter (CPU > 50%)

# sed
sed 's/old/new/' file        # Replace (pierwsza)
sed 's/old/new/g' file       # Replace (wszystkie)
sed -i 's/old/new/g' file    # In-place edit
sed -n '10,20p' file         # Print linie 10-20
sed '/pattern/d' file        # Delete linie z pattern

# cut
cut -d: -f1 /etc/passwd      # Pierwsza kolumna (delimiter :)
echo "one,two,three" | cut -d, -f2  # two

# sort & uniq
sort file
sort -r file                 # Reverse
sort -n file                 # Numeric
sort -u file                 # Unique
uniq file                    # Remove duplicates (wymaga sort)
sort file | uniq -c          # Count duplicates
```

### Process Management

```bash
# ps
ps aux                       # Wszystkie procesy
ps aux | grep process
ps -ef --forest              # Tree view

# top/htop
top                          # Monitor procesów
htop                         # Lepszy top (jeśli zainstalowane)
btop                         # Jeszcze lepszy (jeśli zainstalowane)

# kill
kill PID                     # SIGTERM
kill -9 PID                  # SIGKILL (force)
kill -15 PID                 # SIGTERM (graceful)
killall process_name         # Kill po nazwie
pkill pattern                # Kill po pattern

# jobs & bg/fg
command &                    # Uruchom w tle
jobs                         # Lista zadań
fg %1                        # Przywróć zadanie 1 na pierwszy plan
bg %1                        # Wznów zadanie 1 w tle
Ctrl+z                       # Zawieś proces
bg                           # Wznów w tle

# nohup
nohup command &              # Uruchom, przetrwa logout
```

### System Information

```bash
# Disk
df -h                        # Disk space
du -sh *                     # Rozmiar folderów
du -h --max-depth=1          # Jeden poziom
ncdu                         # Interactive disk usage (jeśli zainstalowane)

# Memory
free -h
cat /proc/meminfo

# CPU
lscpu
cat /proc/cpuinfo
nproc                        # Liczba core'ów

# System
uname -a                     # Kernel info
hostnamectl                  # System info
lsb_release -a               # Distribution info
uptime                       # Uptime i load
```

## Loops w Command Line

```bash
# For loop
for i in {1..5}; do echo $i; done
for file in *.txt; do echo $file; done
for i in $(ls); do echo $i; done

# While loop
while read line; do echo $line; done < file.txt
while true; do echo "running"; sleep 1; done

# One-liners
find . -name "*.txt" -exec echo {} \;
ls | xargs -I {} echo "File: {}"
```

## Przydatne Funkcje (Dodaj do ~/.bashrc)

### 1. Directory i File Management

```bash
# Utwórz katalog i cd do niego
mkcd() {
    mkdir -p "$1" && cd "$1"
}

# Extract dowolnego archiwum
extract() {
    if [ -f $1 ] ; then
        case $1 in
            *.tar.bz2)   tar xjf $1     ;;
            *.tar.gz)    tar xzf $1     ;;
            *.bz2)       bunzip2 $1     ;;
            *.rar)       unrar e $1     ;;
            *.gz)        gunzip $1      ;;
            *.tar)       tar xf $1      ;;
            *.tbz2)      tar xjf $1     ;;
            *.tgz)       tar xzf $1     ;;
            *.zip)       unzip $1       ;;
            *.Z)         uncompress $1  ;;
            *.7z)        7z x $1        ;;
            *)           echo "'$1' nie może być rozpakowane przez extract()" ;;
        esac
    else
        echo "'$1' nie jest prawidłowym plikiem"
    fi
}

# Szybki backup
backup() {
    cp "$1"{,.bak}
}

# Znajdź i zamień w wielu plikach
findreplace() {
    find . -type f -exec sed -i "s/$1/$2/g" {} +
}
```

### 2. Network

```bash
# Mój publiczny IP
myip() {
    curl -s ifconfig.me
}

# Sprawdź port
port() {
    sudo lsof -i :$1
}

# Ping uproszczony
p() {
    ping -c 5 $1
}
```

### 3. Git Helpers

```bash
# Git commit i push
gcp() {
    git add .
    git commit -m "$1"
    git push
}

# Git status krótko
gs() {
    git status -sb
}

# Clone i cd
gclone() {
    git clone "$1" && cd "$(basename "$1" .git)"
}
```

### 4. Produktywność

```bash
# Policz pliki w katalogu
count() {
    find ${1:-.} -type f | wc -l
}

# Rozmiar folderu
size() {
    du -sh ${1:-.}
}

# Szybkie notatki
note() {
    echo "$(date '+%Y-%m-%d %H:%M:%S'): $*" >> ~/notes.txt
}

# Zobacz notatki
notes() {
    cat ~/notes.txt
}
```

### 5. Process Management

```bash
# Znajdź proces i zabij
pskill() {
    ps aux | grep -v grep | grep -i -e "$1" | awk '{print $2}' | xargs kill -9
}

# Watch command co sekundę
watch() {
    while true; do
        clear
        $@
        sleep 1
    done
}
```

## Przydatne Aliasy

Dodaj do `~/.bashrc`:

```bash
# Nawigacja
alias ..='cd ..'
alias ...='cd ../..'
alias ....='cd ../../..'
alias .....='cd ../../../..'
alias ~='cd ~'
alias -- -='cd -'

# ls enhanced (z eza w Omakub)
alias ls='eza'
alias ll='eza -lh'
alias la='eza -lah'
alias lt='eza --tree'
alias l='eza -lah'

# Bezpieczeństwo
alias rm='rm -i'
alias cp='cp -i'
alias mv='mv -i'
alias ln='ln -i'

# Git
alias g='git'
alias gs='git status'
alias ga='git add'
alias gc='git commit'
alias gp='git push'
alias gl='git pull'
alias gd='git diff'
alias gco='git checkout'
alias gb='git branch'

# Grep z kolorami
alias grep='grep --color=auto'
alias fgrep='fgrep --color=auto'
alias egrep='egrep --color=auto'

# System
alias update='sudo apt update && sudo apt upgrade'
alias install='sudo apt install'
alias remove='sudo apt remove'
alias search='apt search'

# Shortcuts
alias h='history'
alias j='jobs -l'
alias c='clear'
alias e='nvim'
alias v='nvim'

# Network
alias ports='netstat -tulanp'
alias myip='curl ifconfig.me'
alias speedtest='curl -s https://raw.githubusercontent.com/sivel/speedtest-cli/master/speedtest.py | python -'

# Processes
alias psg='ps aux | grep -v grep | grep -i -e VSZ -e'
alias cpu='top -o %CPU'
alias mem='top -o %MEM'

# Misc
alias now='date +"%Y-%m-%d %H:%M:%S"'
alias timestamp='date +%s'
alias week='date +%V'
alias path='echo -e ${PATH//:/\\n}'
alias mounted='mount | column -t'
```

## .bashrc Produktywność Booster

Kompletna sekcja do dodania do `~/.bashrc`:

```bash
# ============================================
# PRODUCTIVITY ENHANCEMENTS
# ============================================

# Better command history
export HISTSIZE=10000
export HISTFILESIZE=20000
export HISTCONTROL=ignoreboth:erasedups
export HISTIGNORE="ls:ll:cd:pwd:exit:clear:history"
export HISTTIMEFORMAT="%F %T "
shopt -s histappend
PROMPT_COMMAND="history -a; $PROMPT_COMMAND"

# Better directory navigation
shopt -s autocd          # cd wpisując samą nazwę folderu
shopt -s cdspell         # Poprawiaj literówki w cd
shopt -s dirspell        # Poprawiaj literówki w autocomplete

# Globbing
shopt -s globstar        # ** dla recursive glob
shopt -s nocaseglob      # Case insensitive glob

# Better tab completion
bind 'set completion-ignore-case on'
bind 'set show-all-if-ambiguous on'
bind 'set colored-stats on'
bind 'set mark-symlinked-directories on'

# Custom prompt (minimalistyczny)
PS1='\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '

# Dodaj wszystkie funkcje i aliasy z poprzednich sekcji...
```

## Zasoby

- **Bash Manual:** `man bash`
- **Readline Manual:** `man readline`
- **Advanced Bash Scripting:** https://tldp.org/LDP/abs/html/
- **Bash Cheatsheet:** https://devhints.io/bash
- **ShellCheck:** https://www.shellcheck.net/ (sprawdź skrypty)

## Szybki Start

**Najważniejsze skróty:**
- `Ctrl+r` - Szukaj w historii (fzf!)
- `Ctrl+a/e` - Początek/koniec linii
- `Alt+.` - Ostatni argument
- `!!` - Poprzednia komenda
- `!$` - Ostatni argument
- `Ctrl+l` - Clear screen

**Zapamiętaj:**
- Wszystko można pipe'ować
- Używaj tab completion
- Historia to Twój przyjaciel
- Funkcje i aliasy oszczędzają czas
- `man` jest Twoim przyjacielem
