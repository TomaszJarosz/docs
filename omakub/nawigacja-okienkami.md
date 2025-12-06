# Cheatsheet - Nawigacja Okienkami

## Podstawowe Skróty Okien (GNOME/Ubuntu)

### Zarządzanie Oknami
- `Super + ←/→` - Przypnij okno do lewej/prawej strony ekranu (snap)
- `Super + ↑` - Maksymalizuj okno
- `Super + ↓` - Przywróć/minimalizuj okno
- `Alt + F4` - Zamknij okno
- `Alt + F10` - Przełącz maksymalizację okna
- `Alt + F8` - Zmień rozmiar okna (strzałkami)
- `Alt + F7` - Przesuń okno (strzałkami)
- `Alt + Space` - Menu okna

### Przełączanie Między Oknami
- `Alt + Tab` - Przełącz między oknami
- `Alt + Shift + Tab` - Przełącz między oknami (wstecz)
- `Alt + \`` (backtick) - Przełącz między oknami tej samej aplikacji
- `Super + Tab` - Przełącz między aplikacjami (z podglądem)
- `Ctrl + Alt + Tab` - Przełącz fokus między panelami a oknami

### Workspaces (Obszary Robocze)
- `Super + Page Up/Down` - Przełącz między workspaces
- `Ctrl + Alt + ↑/↓` - Przełącz między workspaces (alternatywnie)
- `Super + Shift + Page Up/Down` - Przenieś okno do innego workspace
- `Ctrl + Alt + Shift + ↑/↓` - Przenieś okno do innego workspace (alternatywnie)

### Multi-Monitor (Wiele Monitorów)
- `Super + Shift + ←/→` - Przesuń okno do monitora po lewej/prawej
- `Super + P` - Projektor/ustawienia ekranu (wyświetl opcje monitorów)
- `Alt + F7` następnie `Shift + ←/→` - Przesuń okno między monitorami (po aktywacji trybu przenoszenia)

**Metody przesunięcia okna między monitorami:**

1. **Skrót klawiszowy (najszybsza metoda):**
   - `Super + Shift + ←` - Przesuń na lewy monitor
   - `Super + Shift + →` - Przesuń na prawy monitor

2. **Przeciąganie myszką:**
   - Chwyt za pasek tytułu i przeciągnij
   - Tip: przytrzymaj `Super` podczas przeciągania dla płynniejszego ruchu

3. **Menu okna:**
   - `Alt + Space` → wybierz "Przenieś na ekran..." → wybierz monitor

4. **Via GNOME Settings:**
   - Wejdź w `Settings` → `Displays` aby skonfigurować pozycje monitorów
   - Poprawna konfiguracja ułatwia przeciąganie okien

**Dobre praktyki multi-monitor:**
- Ustaw główny monitor (primary) - tam pojawią się nowe okna
- Używaj różnych workspaces na każdym monitorze dla lepszej organizacji
- Konsekwentnie umieszczaj określone typy aplikacji na określonych monitorach
  - Przykład: kod na lewym, dokumentacja na prawym
  - Przykład: terminal na głównym, logi/monitoring na dodatkowym

### Przegląd i Wyszukiwanie
- `Super` - Otwórz Activities Overview (widok wszystkich okien)
- `Super + A` - Pokaż aplikacje
- `Super + S` - Szybki przegląd wszystkich workspaces

## Terminal Multiplexer (tmux)

### Sesje
- `tmux new -s nazwa` - Utwórz nową sesję
- `tmux ls` - Lista sesji
- `tmux attach -t nazwa` - Dołącz do sesji
- `Ctrl + B, D` - Odłącz od sesji (detach)
- `Ctrl + B, $` - Zmień nazwę sesji

### Okna (Windows)
- `Ctrl + B, C` - Utwórz nowe okno
- `Ctrl + B, N` - Następne okno
- `Ctrl + B, P` - Poprzednie okno
- `Ctrl + B, 0-9` - Przejdź do okna o numerze
- `Ctrl + B, ,` - Zmień nazwę okna
- `Ctrl + B, &` - Zamknij okno (z potwierdzeniem)
- `Ctrl + B, W` - Lista okien (interactive)

### Panele (Panes)
- `Ctrl + B, %` - Podziel pionowo
- `Ctrl + B, "` - Podziel poziomo
- `Ctrl + B, ←/→/↑/↓` - Przełącz między panelami
- `Ctrl + B, O` - Następny panel (cyklicznie)
- `Ctrl + B, Q` - Pokaż numery paneli
- `Ctrl + B, X` - Zamknij panel
- `Ctrl + B, Z` - Przełącz zoom na panelu (fullscreen/restore)
- `Ctrl + B, Space` - Zmień układ paneli
- `Ctrl + B, {` - Zamień panel z poprzednim
- `Ctrl + B, }` - Zamień panel z następnym
- `Ctrl + B, Ctrl + ←/→/↑/↓` - Zmień rozmiar panelu

### Dodatkowe
- `Ctrl + B, [` - Tryb kopiowania/scrollowania (q aby wyjść)
- `Ctrl + B, :` - Wiersz poleceń tmux
- `Ctrl + B, T` - Pokaż zegar

## Screen (Alternatywa dla tmux)

- `Ctrl + A, C` - Nowe okno
- `Ctrl + A, N` - Następne okno
- `Ctrl + A, P` - Poprzednie okno
- `Ctrl + A, "` - Lista okien
- `Ctrl + A, D` - Detach
- `Ctrl + A, |` - Podziel pionowo
- `Ctrl + A, S` - Podziel poziomo
- `Ctrl + A, Tab` - Przełącz między panelami

## Dobre Praktyki

### Organizacja Workspace
1. **Dedykowane workspaces dla różnych zadań**
   - Workspace 1: Przeglądarka i komunikacja
   - Workspace 2: Terminal i kod
   - Workspace 3: Dokumentacja
   - Workspace 4: Inne narzędzia

2. **Nazywaj okna tmux**
   - Ułatwia identyfikację i szybkie przełączanie
   - `Ctrl + B, ,` aby zmienić nazwę

3. **Grupuj sesje tmux według projektów**
   ```bash
   tmux new -s projekt-frontend
   tmux new -s projekt-backend
   tmux new -s monitoring
   ```

### Efektywna Praca
1. **Używaj snap window (Super + ←/→)**
   - Szybko porównuj dokumenty side-by-side
   - Idealne do code review

2. **Minimalizuj przełączanie kontekstu**
   - Trzymaj związane okna w tym samym workspace
   - Używaj tmux do terminali zamiast wielu osobnych okien

3. **Skróty klawiszowe > mysz**
   - Naucz się podstawowych skrótów
   - Oszczędzasz czas i koncentrację

4. **Sessje tmux dla długotrwałych zadań**
   - Możesz odłączyć się i wrócić później
   - Przetrwają restart SSH
   - Zachowują stan wszystkich procesów

### Workflow z tmux
```bash
# Standardowy workflow deweloperski
# Okno 1: Edytor (vim/nano)
# Okno 2: Serwer deweloperski
# Okno 3: Git i testy
# Okno 4: Monitorowanie logów
```

### Customizacja tmux
Dodaj do `~/.tmux.conf`:
```bash
# Łatwiejsza nawigacja między panelami (bez Ctrl+B)
bind -n M-Left select-pane -L
bind -n M-Right select-pane -R
bind -n M-Up select-pane -U
bind -n M-Down select-pane -D

# Rozpocznij numerację od 1 (łatwiej na klawiaturze)
set -g base-index 1
setw -g pane-base-index 1

# Szybszy prefix (opcjonalnie)
# set -g prefix C-a
# unbind C-b
# bind C-a send-prefix
```

## Szybkie Polecenia

### Tworzenie Środowiska Pracy
```bash
# Nowa sesja z oknem podzielonym na 3 panele
tmux new-session \; \
  split-window -h \; \
  split-window -v \; \
  select-pane -t 0
```

### Zapisz i Przywróć Sesje (tmux-resurrect)
```bash
# Instalacja
git clone https://github.com/tmux-plugins/tmux-resurrect ~/.tmux/plugins/tmux-resurrect

# W ~/.tmux.conf dodaj:
# run-shell ~/.tmux/plugins/tmux-resurrect/resurrect.tmux

# Zapisz: Ctrl + B, Ctrl + S
# Przywróć: Ctrl + B, Ctrl + R
```

## Przydatne Aliasy

Dodaj do `~/.bashrc` lub `~/.zshrc`:
```bash
alias tl='tmux ls'
alias ta='tmux attach -t'
alias tn='tmux new -s'
alias tk='tmux kill-session -t'
```

## Rozwiązywanie Problemów

### Gubisz się w oknach?
- Używaj `Ctrl + B, W` w tmux aby zobaczyć interaktywną listę
- Nazywaj wszystkie okna (szczególnie w tmux)
- Używaj nie więcej niż 4-5 okien na sesję

### Za dużo paneli?
- `Ctrl + B, Z` aby skupić się na jednym panelu
- Rozważ osobne okna zamiast wielu paneli
- Maksymalnie 3-4 panele w jednym oknie

### Konflikty skrótów?
- Sprawdź `dconf-editor` dla GNOME
- Customizuj prefix w tmux jeśli koliduje z innymi skrótami
- Dokumentuj swoje zmiany

## Zasoby

- [tmux cheatsheet](https://tmuxcheatsheet.com/)
- [GNOME Keyboard Shortcuts](https://help.gnome.org/users/gnome-help/stable/shell-keyboard-shortcuts.html)
- `man tmux` - Pełna dokumentacja tmux
- `tmux list-keys` - Lista wszystkich bindingów w tmux
