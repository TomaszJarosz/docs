# Shell Productivity - Cheatsheet

Advanced tricks and shortcuts for productive work in bash/shell.

## Bash Keyboard Shortcuts

### Line Navigation

| Shortcut | Action |
|-------|-------|
| `Ctrl+a` | Beginning of line |
| `Ctrl+e` | End of line |
| `Alt+f` | Word forward |
| `Alt+b` | Word backward |
| `Ctrl+xx` | Toggle between beginning and current position |

### Editing

| Shortcut | Action |
|-------|-------|
| `Ctrl+k` | Cut to end of line |
| `Ctrl+u` | Cut to beginning of line |
| `Alt+d` | Cut word forward |
| `Alt+Backspace` | Cut word backward |
| `Ctrl+w` | Cut word backward (to space) |
| `Ctrl+y` | Paste last cut |
| `Alt+t` | Swap last 2 words |
| `Ctrl+t` | Swap last 2 characters |
| `Alt+u` | Uppercase word |
| `Alt+l` | Lowercase word |
| `Alt+c` | Capitalize word |

### Command History

| Shortcut | Action |
|-------|-------|
| `Ctrl+r` | Search history (fzf in Omakub!) |
| `Ctrl+s` | Search forward (after Ctrl+r) |
| `Ctrl+p` | Previous command |
| `Ctrl+n` | Next command |
| `Alt+.` | Last argument of previous command |
| `Alt+Shift+.` | First argument of previous command |
| `!!` | Previous command |
| `!$` | Last argument |
| `!^` | First argument |
| `!*` | All arguments |
| `!n` | Command number n from history |
| `!-n` | nth command from the end |
| `!string` | Last command starting with string |
| `!?string` | Last command containing string |

### Control

| Shortcut | Action |
|-------|-------|
| `Ctrl+l` | Clear screen (like `clear`) |
| `Ctrl+c` | Interrupt command (SIGINT) |
| `Ctrl+d` | Exit shell / EOF |
| `Ctrl+z` | Suspend process (bg to resume in background) |
| `Ctrl+s` | Stop output (scroll lock) |
| `Ctrl+q` | Resume output |

### Tab Completion

| Shortcut | Action |
|-------|-------|
| `Tab` | Autocomplete |
| `Tab Tab` | Show all possibilities |
| `Alt+/` | Complete filename |
| `Alt+~` | Complete username |
| `Alt+$` | Complete variable |
| `Alt+@` | Complete hostname |
| `Alt+*` | Insert all completions |

## Command History

### Basics

```bash
# View history
history

# Last 10 commands
history 10

# Search in history
history | grep keyword

# Clear history
history -c

# Delete specific entry
history -d 123
```

### History Expansion

```bash
# Execute last command
!!

# Execute as sudo
sudo !!

# Last argument
ls /long/path/to/file
cd !$              # cd /long/path/to/file

# All arguments
command arg1 arg2 arg3
another !*         # another arg1 arg2 arg3

# Change in last command
!!:s/old/new       # Replace old with new
^old^new           # Shorter form

# Example:
vim /etc/config
^vim^cat           # Executes: cat /etc/config
```

### History Configuration

Add to `~/.bashrc`:
```bash
# History size
export HISTSIZE=10000
export HISTFILESIZE=20000

# Ignore duplicates and commands starting with space
export HISTCONTROL=ignoreboth:erasedups

# Ignore specific commands
export HISTIGNORE="ls:ll:cd:pwd:exit:clear"

# Timestamp in history
export HISTTIMEFORMAT="%F %T "

# Append instead of overwrite
shopt -s histappend

# Save immediately (for multiple terminals)
PROMPT_COMMAND="history -a; $PROMPT_COMMAND"
```

## Brace Expansion

```bash
# Range
echo {1..10}              # 1 2 3 4 5 6 7 8 9 10
echo {a..z}               # a b c d ... z
echo {01..10}             # 01 02 03 ... 10

# List
echo {jpg,png,gif}        # jpg png gif
mkdir {src,dist,test}     # Creates 3 folders

# Combinations
touch file{1..3}.{js,css}
# Creates: file1.js file1.css file2.js file2.css file3.js file3.css

# Nested
mkdir -p project/{src/{js,css},dist,test}

# Backup
cp file.txt{,.bak}        # cp file.txt file.txt.bak

# Range with increment
echo {0..100..10}         # 0 10 20 30 ... 100
```

## Parameter Expansion

```bash
# Basics
echo $VAR
echo ${VAR}

# Length
echo ${#VAR}

# Substring
VAR="Hello World"
echo ${VAR:0:5}           # Hello
echo ${VAR:6}             # World

# Replacement
echo ${VAR/World/Bash}    # Hello Bash (first)
echo ${VAR//o/0}          # Hell0 W0rld (all)

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

## Command Substitution and Piping

### Command Substitution

```bash
# Modern syntax (preferred)
$(command)

# Old syntax
`command`

# Examples:
echo "Today is $(date)"
files=$(ls | wc -l)
current_dir=$(pwd)

# Nested
echo "Files: $(echo $(ls | wc -l))"
```

### Piping & Redirection

```bash
# Basic
command1 | command2       # Pipe output
command > file            # Redirect output (overwrite)
command >> file           # Append output
command < file            # Input from file
command 2> file           # Redirect stderr
command &> file           # Redirect stdout and stderr
command 2>&1              # Redirect stderr to stdout

# Useful combinations:
# Redirect stdout and stderr to different files
command > stdout.log 2> stderr.log

# Redirect stderr to stdout and pipe
command 2>&1 | grep error

# Ignore output
command > /dev/null
command &> /dev/null

# Tee - save and display
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

## Useful Commands

### Directory Navigation

```bash
# cd tricks
cd -                      # Previous directory
cd                        # Home directory
cd ~user                  # User's home
cd ../..                  # Two levels up

# pushd/popd/dirs
pushd /tmp               # Go to /tmp and remember
pushd /var               # Go to /var
dirs -v                  # Show stack
popd                     # Return to previous

# Aliases in ~/.bashrc:
alias ..='cd ..'
alias ...='cd ../..'
alias ....='cd ../../..'
```

### Finding Files

```bash
# find
find . -name "*.txt"
find . -type f -name "*.js"
find . -mtime -7              # Modified in last 7 days
find . -size +10M             # Larger than 10MB
find . -name "*.log" -delete  # Find and delete

# fd (more modern, faster)
fd pattern
fd -e txt                     # Extension
fd -t f                       # Type file
fd -H                         # Include hidden
fd pattern -x rm              # Execute command

# locate (fast, but requires updatedb)
locate filename
updatedb                      # Update database (sudo)
```

### Text Processing

```bash
# grep
grep pattern file
grep -r pattern dir          # Recursive
grep -i pattern file         # Case insensitive
grep -v pattern file         # Invert (doesn't contain)
grep -n pattern file         # With line numbers
grep -c pattern file         # Count matches
grep -A 3 pattern file       # 3 lines after
grep -B 3 pattern file       # 3 lines before
grep -C 3 pattern file       # 3 lines before and after

# ripgrep (rg - faster)
rg pattern
rg -i pattern                # Case insensitive
rg -t py pattern             # Only Python files
rg -l pattern                # Only file names

# awk
awk '{print $1}' file        # First column
awk -F: '{print $1}' file    # Custom delimiter
ps aux | awk '$3 > 50'       # Filter (CPU > 50%)

# sed
sed 's/old/new/' file        # Replace (first)
sed 's/old/new/g' file       # Replace (all)
sed -i 's/old/new/g' file    # In-place edit
sed -n '10,20p' file         # Print lines 10-20
sed '/pattern/d' file        # Delete lines with pattern

# cut
cut -d: -f1 /etc/passwd      # First column (delimiter :)
echo "one,two,three" | cut -d, -f2  # two

# sort & uniq
sort file
sort -r file                 # Reverse
sort -n file                 # Numeric
sort -u file                 # Unique
uniq file                    # Remove duplicates (requires sort)
sort file | uniq -c          # Count duplicates
```

### Process Management

```bash
# ps
ps aux                       # All processes
ps aux | grep process
ps -ef --forest              # Tree view

# top/htop
top                          # Process monitor
htop                         # Better top (if installed)
btop                         # Even better (if installed)

# kill
kill PID                     # SIGTERM
kill -9 PID                  # SIGKILL (force)
kill -15 PID                 # SIGTERM (graceful)
killall process_name         # Kill by name
pkill pattern                # Kill by pattern

# jobs & bg/fg
command &                    # Run in background
jobs                         # List jobs
fg %1                        # Bring job 1 to foreground
bg %1                        # Resume job 1 in background
Ctrl+z                       # Suspend process
bg                           # Resume in background

# nohup
nohup command &              # Run, survives logout
```

### System Information

```bash
# Disk
df -h                        # Disk space
du -sh *                     # Folder sizes
du -h --max-depth=1          # One level
ncdu                         # Interactive disk usage (if installed)

# Memory
free -h
cat /proc/meminfo

# CPU
lscpu
cat /proc/cpuinfo
nproc                        # Number of cores

# System
uname -a                     # Kernel info
hostnamectl                  # System info
lsb_release -a               # Distribution info
uptime                       # Uptime and load
```

## Loops on Command Line

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

## Useful Functions (Add to ~/.bashrc)

### 1. Directory and File Management

```bash
# Create directory and cd into it
mkcd() {
    mkdir -p "$1" && cd "$1"
}

# Extract any archive
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
            *)           echo "'$1' cannot be extracted via extract()" ;;
        esac
    else
        echo "'$1' is not a valid file"
    fi
}

# Quick backup
backup() {
    cp "$1"{,.bak}
}

# Find and replace in multiple files
findreplace() {
    find . -type f -exec sed -i "s/$1/$2/g" {} +
}
```

### 2. Network

```bash
# My public IP
myip() {
    curl -s ifconfig.me
}

# Check port
port() {
    sudo lsof -i :$1
}

# Simplified ping
p() {
    ping -c 5 $1
}
```

### 3. Git Helpers

```bash
# Git commit and push
gcp() {
    git add .
    git commit -m "$1"
    git push
}

# Git status short
gs() {
    git status -sb
}

# Clone and cd
gclone() {
    git clone "$1" && cd "$(basename "$1" .git)"
}
```

### 4. Productivity

```bash
# Count files in directory
count() {
    find ${1:-.} -type f | wc -l
}

# Folder size
size() {
    du -sh ${1:-.}
}

# Quick notes
note() {
    echo "$(date '+%Y-%m-%d %H:%M:%S'): $*" >> ~/notes.txt
}

# View notes
notes() {
    cat ~/notes.txt
}
```

### 5. Process Management

```bash
# Find process and kill
pskill() {
    ps aux | grep -v grep | grep -i -e "$1" | awk '{print $2}' | xargs kill -9
}

# Watch command every second
watch() {
    while true; do
        clear
        $@
        sleep 1
    done
}
```

## Useful Aliases

Add to `~/.bashrc`:

```bash
# Navigation
alias ..='cd ..'
alias ...='cd ../..'
alias ....='cd ../../..'
alias .....='cd ../../../..'
alias ~='cd ~'
alias -- -='cd -'

# ls enhanced (with eza in Omakub)
alias ls='eza'
alias ll='eza -lh'
alias la='eza -lah'
alias lt='eza --tree'
alias l='eza -lah'

# Safety
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

# Grep with colors
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

## .bashrc Productivity Booster

Complete section to add to `~/.bashrc`:

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
shopt -s autocd          # cd by typing just folder name
shopt -s cdspell         # Fix typos in cd
shopt -s dirspell        # Fix typos in autocomplete

# Globbing
shopt -s globstar        # ** for recursive glob
shopt -s nocaseglob      # Case insensitive glob

# Better tab completion
bind 'set completion-ignore-case on'
bind 'set show-all-if-ambiguous on'
bind 'set colored-stats on'
bind 'set mark-symlinked-directories on'

# Custom prompt (minimalist)
PS1='\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '

# Add all functions and aliases from previous sections...
```

## Resources

- **Bash Manual:** `man bash`
- **Readline Manual:** `man readline`
- **Advanced Bash Scripting:** https://tldp.org/LDP/abs/html/
- **Bash Cheatsheet:** https://devhints.io/bash
- **ShellCheck:** https://www.shellcheck.net/ (check scripts)

## Quick Start

**Most important shortcuts:**
- `Ctrl+r` - Search history (fzf!)
- `Ctrl+a/e` - Beginning/end of line
- `Alt+.` - Last argument
- `!!` - Previous command
- `!$` - Last argument
- `Ctrl+l` - Clear screen

**Remember:**
- Everything can be piped
- Use tab completion
- History is your friend
- Functions and aliases save time
- `man` is your friend
