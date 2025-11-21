# Omakub Cheatsheet

Omakub to kompletny setup dla Ubuntu od Basecamp - zestaw narzędzi i konfiguracji dla produktywnej pracy.

**Oficjalna strona:** https://omakub.org/

## Komponenty Omakub

- 🖥️ **Terminal:** Zellij (multiplexer)
- ✏️ **Edytor:** Neovim z LazyVim
- 🚀 **Launcher:** Ulauncher
- 🐚 **Shell:** Bash z konfiguracją
- 🔧 **Narzędzia:** fzf, ripgrep, eza, bat, lazygit i więcej

## Launcher - Ulauncher

**Główny skrót:** `Super+Space` (Windows key + Space)

### Podstawowe Użycie
| Akcja | Jak |
|-------|-----|
| Otwórz launcher | `Super+Space` |
| Uruchom aplikację | Wpisz nazwę → `Enter` |
| Wyszukaj w Google | `g query` |
| Kalkulator | Wpisz wyrażenie np. `2+2` |

### Dostępne Skróty w Launcherze
- `g <query>` - Google search
- `gh <repo>` - Otwórz repo na GitHub
- `so <query>` - Stack Overflow search
- `wiki <query>` - Wikipedia search

### Konfiguracja Ulauncher
```bash
# Otwórz ustawienia
ulauncher-toggle
# Potem: ikona w tray → Preferences
```

## Terminal - Zellij

**Uruchomienie:**
```bash
zellij
```

### Najważniejsze Skróty
| Skrót | Akcja |
|-------|-------|
| `Alt+h/j/k/l` | Nawigacja między panelami |
| `Alt+n` | Nowy panel |
| `Alt+f` | Floating panel |
| `Alt++/-` | Resize panelu |
| `Ctrl+g` | Unlock (normal mode) |

**Zobacz szczegóły:** `~/docs/zellij-cheatsheet.md`

## Edytor - Neovim (LazyVim)

**Uruchomienie:**
```bash
nvim plik.txt
# lub
e plik.txt  # alias w Omakub
```

### Najważniejsze Skróty
| Skrót | Akcja |
|-------|-------|
| `Space` | Leader menu (which-key) |
| `Space+ff` | Find files |
| `Space+sg` | Search in files (grep) |
| `Space+e` | File explorer |
| `Esc` | Normal mode |

**Zobacz szczegóły:** `~/docs/neovim-lazyvim-cheatsheet.md`

## CLI Tools (Omakub Defaults)

### eza (lepszy ls)

Omakub ustawia aliasy dla `ls`:
```bash
ls          # eza z kolorami
ll          # eza -lh (długa lista)
la          # eza -lah (wszystkie pliki)
lt          # eza --tree (drzewo)
```

### bat (lepszy cat)

```bash
bat plik.txt          # Podświetlanie składni
bat plik1 plik2       # Wiele plików
bat --style=plain     # Bez dekoracji
```

### fzf (fuzzy finder)

```bash
# Interaktywne wyszukiwanie plików
Ctrl+T

# Interaktywna historia komend
Ctrl+R

# Zmiana katalogu
Alt+C   # lub cd **<Tab>
```

### ripgrep (rg - szybkie grep)

```bash
rg "pattern"              # Szukaj w plikach
rg "pattern" --type py    # Tylko pliki Python
rg "pattern" -i           # Case insensitive
rg "pattern" -l           # Tylko nazwy plików
```

### lazygit (Git GUI w terminalu)

```bash
lazygit
```

**W lazygit:**
| Skrót | Akcja |
|-------|-------|
| `1-5` | Przełącz między panelami |
| `Space` | Stage/unstage |
| `c` | Commit |
| `P` | Push |
| `p` | Pull |
| `a` | Amend commit |
| `e` | Edit file |
| `o` | Open file |
| `d` | Delete |
| `q` | Quit |

## Aliasy Bash (Omakub)

Sprawdź dostępne aliasy:
```bash
alias
```

### Najczęściej Używane
```bash
# Nawigacja
..          # cd ..
...         # cd ../..
....        # cd ../../..

# Git
g           # git
gs          # git status
ga          # git add
gc          # git commit
gp          # git push
gl          # git pull
gd          # git diff
glog        # git log --oneline --graph

# Edytor
e           # nvim
vim         # nvim

# System
update      # sudo apt update && sudo apt upgrade
ports       # netstat -tulanp
myip        # curl ifconfig.me

# Docker (jeśli zainstalowane)
dc          # docker-compose
```

## Skróty Klawiszowe (Desktop)

### Zarządzanie Oknami
| Skrót | Akcja |
|-------|-------|
| `Super+Space` | Ulauncher |
| `Super+Enter` | Terminal |
| `Super+Q` | Zamknij okno |
| `Super+F` | Fullscreen |
| `Super+H/L` | Tile left/right |
| `Super+↑/↓` | Maximize/Restore |
| `Alt+Tab` | Przełącz okna |
| `Super+Tab` | Przełącz aplikacje |

### Workspaces (Obszary robocze)
| Skrót | Akcja |
|-------|-------|
| `Super+PgUp/PgDn` | Przełącz workspace |
| `Super+Shift+PgUp/PgDn` | Przenieś okno do workspace |

**Uwaga:** Skróty mogą się różnić w zależności od DE (GNOME, KDE, etc.)

## Zarządzanie Pakietami

### apt (system packages)
```bash
sudo apt update              # Aktualizuj listę pakietów
sudo apt upgrade             # Zainstaluj aktualizacje
sudo apt install pakiet      # Zainstaluj pakiet
sudo apt remove pakiet       # Usuń pakiet
sudo apt autoremove          # Usuń niepotrzebne zależności
```

### snap
```bash
snap list                    # Lista zainstalowanych
snap install pakiet          # Zainstaluj
snap remove pakiet           # Usuń
```

### Języki programowania

**Ruby (rbenv):**
```bash
rbenv versions               # Lista wersji
rbenv install 3.2.0          # Zainstaluj wersję
rbenv global 3.2.0           # Ustaw globalnie
rbenv local 3.2.0            # Ustaw dla projektu
```

**Node.js (nvm - jeśli zainstalowane):**
```bash
nvm list                     # Lista wersji
nvm install 20               # Zainstaluj Node 20
nvm use 20                   # Użyj Node 20
nvm alias default 20         # Ustaw domyślnie
```

**Python:**
```bash
python3 --version
pip3 install pakiet
python3 -m venv venv         # Virtual environment
source venv/bin/activate
```

## Konfiguracja Omakub

### Pliki Konfiguracyjne

```bash
~/.bashrc                    # Bash config
~/.config/zellij/            # Zellij config
~/.config/nvim/              # Neovim config
~/.gitconfig                 # Git config
~/.local/share/omakub/       # Omakub defaults
```

### Dostosowanie Bash
```bash
# Edytuj ~/.bashrc
nvim ~/.bashrc

# Przeładuj
source ~/.bashrc
```

### Zmiana Motywu

Omakub ma predefiniowane motywy dla terminala i edytora.

**Terminal theme:**
```bash
# Sprawdź dostępne
ls ~/.local/share/omakub/themes/

# Edytuj konfigurację terminala (zależy od terminala)
```

**Neovim theme:**
```bash
# W Neovim
:Lazy
# Znajdź colorscheme i zmień
```

## Workflow Tips

### 1. Terminal Workflow
```bash
# Uruchom Zellij z named session
zellij -s projekt

# W Zellij:
Alt+n              # Nowy panel
Alt+h/j/k/l        # Nawiguj
Ctrl+g → o → d     # Detach

# Wróć później
zellij attach projekt
```

### 2. Edycja z Neovim
```bash
# Otwórz projekt
cd ~/projekt
e .                # Otwórz nvim w katalogu

# W Neovim:
Space+e            # File explorer
Space+ff           # Find file
Space+sg           # Search in files
```

### 3. Git Workflow
```bash
# W katalogu projektu
lazygit            # Otwórz lazygit

# Lub tradycyjnie:
gs                 # git status
ga .               # git add .
gc -m "message"    # git commit
gp                 # git push
```

### 4. Szybkie Wyszukiwanie
```bash
# Znajdź plik
Ctrl+T             # fzf file search

# Szukaj w historii
Ctrl+R             # fzf command history

# Szukaj w plikach
rg "pattern"       # ripgrep
```

### 5. Multi-projekty z Zellij
```bash
# Projekt 1
zellij -s backend

# Projekt 2 (nowa sesja terminala)
zellij -s frontend

# Lista sesji
zellij list-sessions

# Przełącz się
Ctrl+g → o → w     # Session manager w Zellij
```

## Dostosowanie Omakub

### Dodaj Własne Aliasy
```bash
# Edytuj ~/.bashrc
nvim ~/.bashrc

# Dodaj na końcu:
alias myalias='command'

# Przeładuj
source ~/.bashrc
```

### Dodaj Własne Funkcje
```bash
# W ~/.bashrc
function mkcd() {
    mkdir -p "$1" && cd "$1"
}

# Użycie:
mkcd nowy-folder
```

### Instalacja Dodatkowych Narzędzi
```bash
# Przykład: tldr (simplified man pages)
sudo apt install tldr
tldr ls

# Przykład: httpie (HTTP client)
sudo apt install httpie
http GET https://api.github.com
```

## System Maintenance

### Aktualizacja Systemu
```bash
# Pełna aktualizacja
sudo apt update && sudo apt upgrade -y

# Czyszczenie
sudo apt autoremove
sudo apt autoclean
```

### Sprawdzanie Miejsca na Dysku
```bash
df -h              # Partycje
du -sh *           # Rozmiar folderów
ncdu               # Interaktywnie (jeśli zainstalowane)
```

### Monitorowanie Systemu
```bash
htop               # Monitor procesów
btop               # Nowoczesny htop (jeśli zainstalowane)
free -h            # Pamięć
```

## Troubleshooting

### Terminal nie otwiera się
```bash
# Sprawdź domyślny shell
echo $SHELL

# Reset terminala
Ctrl+C lub Ctrl+D
```

### Zellij się zawiesił
```bash
# Zabij wszystkie sesje
zellij delete-all-sessions

# Wyczyść cache
rm -rf ~/.cache/zellij
```

### Neovim działa wolno
```bash
# W Neovim
:Lazy
# Zaktualizuj pluginy: U

# Sprawdź LSP
:LspInfo

# Restart Neovim
:q
nvim
```

### Ulauncher nie działa
```bash
# Restart Ulauncher
ulauncher-toggle

# Sprawdź proces
ps aux | grep ulauncher

# Uruchom ponownie
ulauncher &
```

### F11 wymaga Fn (Problem z fullscreen)

Jeśli musisz wciskać `Fn+F11` zamiast samego `F11`:

**Opcja 1: Zmień w BIOS (zalecane)**
1. Restart → wejdź do BIOS (F2/F10/Del podczas startu)
2. Znajdź opcję "Function Key Behavior" lub "Action Keys Mode"
3. Zmień na "Function Keys" (zamiast "Multimedia Keys")
4. Zapisz i wyjdź

**Opcja 2: Używaj alternatywnych skrótów**
- `Super+↑` - maximize okno
- `Super+F` - fullscreen (w niektórych DE)

**Opcja 3: Zmień skrót w terminalu**
- Otwórz ustawienia terminala
- Keyboard shortcuts
- Zmień fullscreen na inny skrót (np. `Ctrl+Shift+F`)

## Skróty Produktywności

### 1. Szybkie Edytowanie Konfiguracji
```bash
# Bash config
e ~/.bashrc

# Zellij config
e ~/.config/zellij/config.kdl

# Git config
e ~/.gitconfig
```

### 2. Szybka Nawigacja
```bash
# Jump to directories (z)
z projekt          # Skocz do ~/projekty/projekt
                   # (wymaga zainstalowania 'z' lub 'zoxide')

# Marks (bookmarks)
# Dodaj do ~/.bashrc:
export MARKPATH=$HOME/.marks
function jump { cd -P "$MARKPATH/$1" 2>/dev/null || echo "No such mark: $1"; }
function mark { mkdir -p "$MARKPATH"; ln -s "$(pwd)" "$MARKPATH/$1"; }
function unmark { rm -i "$MARKPATH/$1"; }
function marks { ls -l "$MARKPATH" | tail -n +2 | cut -d' ' -f9- ; }
```

### 3. Clipboard Magic
```bash
# Kopiuj output do schowka
command | xclip -selection clipboard

# Lub (jeśli zainstalowane)
command | pbcopy   # macOS style

# Alias w ~/.bashrc:
alias c='xclip -selection clipboard'

# Użycie:
cat file.txt | c
```

## Zasoby

- **Omakub Docs:** https://omakub.org/
- **Omakub GitHub:** https://github.com/basecamp/omakub
- **Zellij Docs:** https://zellij.dev/
- **LazyVim Docs:** https://www.lazyvim.org/
- **Ubuntu Docs:** https://help.ubuntu.com/

---

## Szybki Start

**Pierwszy dzień z Omakub:**

1. **Uruchom terminal:**
   ```bash
   Super+Enter
   ```

2. **Zellij session:**
   ```bash
   zellij -s work
   ```

3. **Podziel panel:**
   ```bash
   Alt+n           # Nowy panel
   Alt+h/j/k/l     # Poruszaj się
   ```

4. **Otwórz projekt:**
   ```bash
   cd ~/projekt
   e .             # Neovim
   ```

5. **Launcher:**
   ```bash
   Super+Space
   ```

6. **Git workflow:**
   ```bash
   lazygit
   ```

**Zapamiętaj:**
- `Super+Space` - uruchom co chcesz (Ulauncher)
- `Alt+...` - steruj Zellij
- `Space` - leader w Neovim
- `Ctrl+R` - historia komend
- `Ctrl+T` - znajdź plik

**Have fun! 🚀**
