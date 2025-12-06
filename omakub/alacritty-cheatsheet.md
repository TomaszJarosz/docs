# Alacritty - Cheatsheet

## Podstawowe Informacje

Alacritty to szybki, minimalistyczny emulator terminala napisany w Rust. Charakteryzuje się:
- Akceleracja GPU dla maksymalnej wydajności
- Minimalistyczny design (brak wbudowanych tabów/paneli)
- Konfiguracja przez plik YAML
- Cross-platform (Linux, macOS, Windows)

## Zarządzanie Oknami

### Podstawowe Operacje
- `Ctrl + Shift + N` - Nowe okno Alacritty
- `Ctrl + Shift + Enter` - Nowe okno (alternatywnie, zależy od konfiguracji)
- `Ctrl + Shift + Q` - Zamknij okno
- `Ctrl + D` - Zamknij terminal (exit shell)
- Z terminala: `alacritty` - Otwórz nowe okno
- `alacritty --working-directory /ścieżka` - Otwórz w konkretnym katalogu
- `alacritty -e vim plik.txt` - Otwórz i wykonaj komendę

### Tryb Fullscreen
- `F11` - Przełącz tryb pełnoekranowy (zależy od konfiguracji)
- Można skonfigurować w `~/.config/alacritty/alacritty.yml`

## Scrollowanie i Nawigacja

### Tryb Vi (Scrollowanie/Kopiowanie)
- `Ctrl + Shift + Space` - Wejdź w tryb vi

**W trybie vi:**
- `k` lub `↑` - Scroll w górę (linia)
- `j` lub `↓` - Scroll w dół (linia)
- `Ctrl + U` - Scroll w górę (pół strony)
- `Ctrl + D` - Scroll w dół (pół strony)
- `Ctrl + B` - Scroll w górę (pełna strona)
- `Ctrl + F` - Scroll w dół (pełna strona)
- `g` - Skok na początek historii
- `G` - Skok na koniec (latest output)
- `h/l` - Lewo/prawo
- `w/b` - Następne/poprzednie słowo
- `0/$` - Początek/koniec linii

**Zaznaczanie i kopiowanie:**
- `v` - Zaznaczanie (visual mode, character)
- `V` - Zaznaczanie linii (visual line mode)
- `Ctrl + V` - Zaznaczanie blokowe (visual block)
- `y` - Kopiuj zaznaczenie do schowka
- `/` - Szukaj do przodu
- `?` - Szukaj do tyłu
- `n/N` - Następne/poprzednie dopasowanie
- `Esc` lub `q` - Wyjście z trybu vi

### Wyszukiwanie
- `Ctrl + Shift + F` - Otwórz pasek wyszukiwania
- `Enter` - Następne dopasowanie
- `Shift + Enter` - Poprzednie dopasowanie
- `Esc` - Zamknij wyszukiwanie

### Schowek
- `Ctrl + Shift + C` - Kopiuj zaznaczenie do schowka
- `Ctrl + Shift + V` - Wklej ze schowka
- `Shift + Insert` - Wklej ze schowka (alternatywnie)
- Zaznaczenie myszką automatycznie kopiuje (opcjonalne, zależy od konfiguracji)

## Czcionka i Wygląd

### Rozmiar Czcionki
- `Ctrl + =` lub `Ctrl + +` - Powiększ czcionkę
- `Ctrl + -` - Zmniejsz czcionkę
- `Ctrl + 0` - Resetuj rozmiar czcionki do domyślnego

## Interakcja z URL i Ścieżkami

- `Ctrl + Shift + B` - Otwórz URL pod kursorem w domyślnej przeglądarce
- `Ctrl + Click` - Otwórz URL (zależy od konfiguracji)
- Hints mode (wymaga konfiguracji):
  - Wyświetla numery przy URL/ścieżkach
  - Wpisz numer aby otworzyć

## Konfiguracja

### Lokalizacja Pliku Konfiguracyjnego
```bash
~/.config/alacritty/alacritty.yml
# lub
~/.config/alacritty/alacritty.toml  # nowsze wersje
```

### Przeładowanie Konfiguracji
- Alacritty automatycznie przeładowuje konfigurację po zapisie
- Nie trzeba restartować terminala
- W razie problemów: zamknij i otwórz ponownie

### Podstawowa Konfiguracja

```yaml
# ~/.config/alacritty/alacritty.yml

# Okno
window:
  opacity: 0.95
  padding:
    x: 10
    y: 10
  decorations: full  # full, none, transparent, buttonless
  startup_mode: Windowed  # Windowed, Maximized, Fullscreen

# Czcionka
font:
  normal:
    family: "JetBrainsMono Nerd Font"
    style: Regular
  bold:
    family: "JetBrainsMono Nerd Font"
    style: Bold
  italic:
    family: "JetBrainsMono Nerd Font"
    style: Italic
  size: 12.0

# Kolory (Tokyo Night przykład)
colors:
  primary:
    background: '#1a1b26'
    foreground: '#c0caf5'
  normal:
    black:   '#15161e'
    red:     '#f7768e'
    green:   '#9ece6a'
    yellow:  '#e0af68'
    blue:    '#7aa2f7'
    magenta: '#bb9af7'
    cyan:    '#7dcfff'
    white:   '#a9b1d6'

# Scrolling
scrolling:
  history: 10000
  multiplier: 3

# Kursor
cursor:
  style:
    shape: Block  # Block, Underline, Beam
    blinking: On
  blink_interval: 750

# Key bindings
key_bindings:
  - { key: Return, mods: Control|Shift, action: SpawnNewInstance }
  - { key: N, mods: Control|Shift, action: SpawnNewInstance }
  - { key: F11, action: ToggleFullscreen }
```

## Dobre Praktyki

### Workflow z Alacritty

**1. Alacritty + tmux (Rekomendowane)**
```bash
# Jedno okno Alacritty, wiele sesji tmux
alacritty -e tmux new-session -A -s main
```
- Alacritty do zarządzania oknami systemowymi
- tmux do zarządzania sesjami/panelami wewnątrz

**2. Wiele Okien Alacritty**
```bash
# Różne okna dla różnych zadań
alacritty --working-directory ~/projekty/frontend &
alacritty --working-directory ~/projekty/backend &
alacritty -e htop &
```

**3. Alacritty na Różnych Workspaces**
- Workspace 1: Alacritty z edytorem (vim/nvim)
- Workspace 2: Alacritty z serwerami deweloperskimi
- Workspace 3: Alacritty z monitoringiem (htop, logs)

### Optymalizacja Wydajności

1. **GPU Rendering**
   - Alacritty używa GPU domyślnie
   - Sprawdź: `alacritty --print-events`

2. **Font Rendering**
   - Używaj czcionek Nerd Font dla ikon
   - Wyłącz ligatury jeśli nie są potrzebne

3. **Historia Scrollback**
   - Ogranicz `scrolling.history` jeśli używasz dużo outputu
   - 10000 linii to dobry balans

### Integracja z Systemem

**Desktop Entry (Launcher)**
```bash
# ~/.local/share/applications/alacritty-custom.desktop
[Desktop Entry]
Type=Application
Name=Alacritty (Project)
Exec=alacritty --working-directory ~/projekty
Icon=Alacritty
Categories=System;TerminalEmulator;
```

**Skrypty Pomocnicze**
```bash
# ~/bin/alacritty-here
#!/bin/bash
# Otwórz Alacritty w bieżącym katalogu
alacritty --working-directory "$(pwd)" &

# Dodaj do ~/.bashrc:
# alias ah='~/bin/alacritty-here'
```

## Porównanie z Innymi Emulatorami

| Feature | Alacritty | GNOME Terminal | Kitty | Terminator |
|---------|-----------|----------------|-------|------------|
| GPU Accel | ✓ | ✗ | ✓ | ✗ |
| Tabs | ✗ | ✓ | ✓ | ✗ |
| Panels | ✗ | ✗ | ✓ | ✓ |
| Config | YAML | GUI | Conf | GUI |
| Speed | Najszybszy | Średni | Szybki | Średni |
| Memory | Niskie | Średnie | Średnie | Wyższe |

**Dlaczego Alacritty?**
- Maksymalna prędkość (GPU rendering)
- Minimalizm (brak bloat)
- Stabilność i przewidywalność
- Doskonała integracja z tmux

**Kiedy NIE używać Alacritty?**
- Potrzebujesz wbudowanych tabów (użyj Kitty)
- Chcesz GUI do konfiguracji (użyj GNOME Terminal)
- Potrzebujesz wbudowanych paneli (użyj Terminator lub Kitty)

## Rozwiązywanie Problemów

### Brak Kolorów w Programach
```bash
# Sprawdź TERM
echo $TERM  # powinno być: alacritty lub xterm-256color

# Jeśli problemy, w ~/.bashrc:
export TERM=xterm-256color
```

### Problemy z Czcionką
```bash
# Lista dostępnych czcionek
fc-list | grep -i "nazwa czcionki"

# Zainstaluj Nerd Fonts
# https://www.nerdfonts.com/
```

### Alacritty Się Nie Uruchamia
```bash
# Sprawdź logi
alacritty -v  # verbose mode

# Testuj konfigurację
alacritty --config-file ~/.config/alacritty/alacritty.yml
```

### Skróty Klawiszowe Nie Działają
- Sprawdź konflikty z systemem (GNOME shortcuts)
- Zdefiniuj własne w `key_bindings` w config
- Użyj `alacritty --print-events` aby zobaczyć przechwytywane zdarzenia

## Przydatne Komendy

```bash
# Informacje o wersji
alacritty --version

# Sprawdź wszystkie opcje
alacritty --help

# Otwórz w trybie debug
alacritty -vvv

# Testuj konfigurację bez wpływu na działające instancje
alacritty --config-file /tmp/test-config.yml

# Wypisz domyślną konfigurację
alacritty migrate  # migruje starą konfigurację do nowej
```

## Zasoby

- [Oficjalna dokumentacja](https://github.com/alacritty/alacritty)
- [Przykłady konfiguracji](https://github.com/alacritty/alacritty/blob/master/alacritty.yml)
- [Color schemes](https://github.com/alacritty/alacritty-theme)
- [Nerd Fonts](https://www.nerdfonts.com/)
- `man alacritty` - Manual page
- `man alacritty-msg` - IPC messaging

## Skróty - Quick Reference

| Akcja | Skrót |
|-------|-------|
| Nowe okno | `Ctrl + Shift + N` |
| Zamknij | `Ctrl + Shift + Q` |
| Tryb Vi | `Ctrl + Shift + Space` |
| Szukaj | `Ctrl + Shift + F` |
| Kopiuj | `Ctrl + Shift + C` |
| Wklej | `Ctrl + Shift + V` |
| Zoom in | `Ctrl + =` |
| Zoom out | `Ctrl + -` |
| Reset zoom | `Ctrl + 0` |
| Otwórz URL | `Ctrl + Shift + B` |
