# Zellij Cheatsheet (Omakub Config)

Zellij to nowoczesny terminal multiplexer - alternatywa dla tmux/screen.

**UWAGA:** Ta konfiguracja jest z **Omakub** i różni się od domyślnej!

## Podstawowe Koncepty

Zellij w Omakub działa w **trybach** (modes) z kluczową różnicą:
- **Domyślnie jesteś w trybie LOCKED** - większość skrótów jest wyłączona!
- `Ctrl+g` przełącza między **locked** ↔ **normal** mode
- W locked mode działają tylko skróty `Alt+...` (najważniejsze!)
- Z normal mode możesz wchodzić w inne tryby (pane, tab, resize, etc.)

## ⭐ Najważniejsze Skróty (Działają Zawsze)

Skróty z **Alt** działają nawet w locked mode:

| Skrót | Akcja |
|-------|-------|
| `Alt+h/j/k/l` lub `Alt+strzałki` | Nawigacja między panelami/tabami |
| `Alt+n` | Nowy panel |
| `Alt+f` | Toggle floating panes |
| `Alt++` | Zwiększ rozmiar panelu |
| `Alt+-` | Zmniejsz rozmiar panelu |
| `Alt+=` | Zwiększ rozmiar panelu |
| `Alt+[` | Poprzedni layout |
| `Alt+]` | Następny layout |
| `Alt+i` | Przenieś tab w lewo |
| `Alt+o` | Przenieś tab w prawo |

## Podstawowe Skróty

### Ogólne
| Skrót | Akcja |
|-------|-------|
| `Ctrl+g` | Przełącz locked ↔ normal mode |
| `Ctrl+q` | Zamknij Zellij (tylko z normal mode) |

## Tryby i Zarządzanie

**UWAGA:** Z locked mode najpierw naciśnij `Ctrl+g` aby przejść do normal mode!

### Panel Mode (z normal: `p`)
Zarządzanie panelami (podziałami ekranu):

| Pełny Skrót | Akcja |
|-------|-------|
| `Ctrl+g` → `p` → `n` | Nowy panel (domyślny kierunek) |
| `Ctrl+g` → `p` → `d` | Panel w dół (horizontal split) |
| `Ctrl+g` → `p` → `r` | Panel w prawo (vertical split) |
| `Ctrl+g` → `p` → `x` | Zamknij aktywny panel |
| `Ctrl+g` → `p` → `f` | **Panel na cały ekran (fullscreen)** ⭐ |
| `Ctrl+g` → `p` → `w` | Przełącz floating panel |
| `Ctrl+g` → `p` → `e` | Embed floating panel |
| `Ctrl+g` → `p` → `c` | Zmień nazwę panelu |
| `Ctrl+g` → `p` → `z` | Toggle panel frames |

**Nawigacja w Panel Mode:**
| Pełny Skrót | Akcja |
|-------|-------|
| `Ctrl+g` → `p` → `h/←` | Przejdź do panelu po lewej |
| `Ctrl+g` → `p` → `l/→` | Przejdź do panelu po prawej |
| `Ctrl+g` → `p` → `j/↓` | Przejdź do panelu poniżej |
| `Ctrl+g` → `p` → `k/↑` | Przejdź do panelu powyżej |
| `Ctrl+g` → `p` → `Tab` | Przełącz focus |

### Resize Mode (z normal: `r`)
Zmiana rozmiaru paneli:

| Pełny Skrót | Akcja |
|-------|-------|
| `Ctrl+g` → `r` → `h/←` | Zwiększ w lewo |
| `Ctrl+g` → `r` → `l/→` | Zwiększ w prawo |
| `Ctrl+g` → `r` → `j/↓` | Zwiększ w dół |
| `Ctrl+g` → `r` → `k/↑` | Zwiększ w górę |
| `Ctrl+g` → `r` → `+` | Zwiększ rozmiar |
| `Ctrl+g` → `r` → `-` | Zmniejsz rozmiar |
| `Ctrl+g` → `r` → `=` | Zwiększ rozmiar (jak +) |
| `Ctrl+g` → `r` → `H/J/K/L` | Zmniejsz w danym kierunku |

💡 **Szybszy sposób:** Użyj `Alt++` lub `Alt+-` bez wchodzenia w tryb!

### Tab Mode (z normal: `t`)
Zarządzanie zakładkami (tabs):

| Pełny Skrót | Akcja |
|-------|-------|
| `Ctrl+g` → `t` → `n` | Nowy tab |
| `Ctrl+g` → `t` → `x` | Zamknij aktywny tab |
| `Ctrl+g` → `t` → `r` | Zmień nazwę taba |
| `Ctrl+g` → `t` → `h/←` | Przejdź do poprzedniego taba |
| `Ctrl+g` → `t` → `l/→` | Przejdź do następnego taba |
| `Ctrl+g` → `t` → `j` | Przejdź do następnego taba |
| `Ctrl+g` → `t` → `k` | Przejdź do poprzedniego taba |
| `Ctrl+g` → `t` → `1-9` | Przejdź do taba numer 1-9 |
| `Ctrl+g` → `t` → `Tab` | Przełącz na ostatnio używany tab |
| `Ctrl+g` → `t` → `s` | Sync tab (synchronizuj input) |
| `Ctrl+g` → `t` → `[` | Break pane left |
| `Ctrl+g` → `t` → `]` | Break pane right |
| `Ctrl+g` → `t` → `b` | Break pane |

### Scroll Mode (z normal: `s`)
Przewijanie i kopiowanie:

| Pełny Skrót | Akcja |
|-------|-------|
| `Ctrl+g` → `s` → `↑/↓` lub `k/j` | Przewijaj w górę/dół |
| `Ctrl+g` → `s` → `PgUp/PgDn` lub `h/l` | Przewijaj stronami |
| `Ctrl+g` → `s` → `u` | Pół strony w górę |
| `Ctrl+g` → `s` → `d` | Pół strony w dół |
| `Ctrl+g` → `s` → `Ctrl+b` | Page scroll up |
| `Ctrl+g` → `s` → `Ctrl+f` | Page scroll down |
| `Ctrl+g` → `s` → `f` | Szukaj (enter search) |
| `Ctrl+g` → `s` → `e` | Edytuj scrollback w edytorze |
| `Ctrl+g` → `s` → `Ctrl+c` | Wyjdź ze scroll mode |

**W Search Mode:**
| Skrót | Akcja |
|-------|-------|
| `n` | Następny wynik |
| `p` | Poprzedni wynik |
| `c` | Toggle case sensitivity |
| `w` | Toggle whole word |
| `o` | Toggle wrap |

Kopiowanie tekstu:
1. Wejdź w Scroll Mode (`Ctrl+g` → `s`)
2. Zaznacz tekst myszką
3. Tekst automatycznie kopiuje się do schowka
4. `Ctrl+c` lub `Esc` aby wyjść

### Session Mode (z normal: `o`)
Zarządzanie sesjami:

| Pełny Skrót | Akcja |
|-------|-------|
| `Ctrl+g` → `o` → `d` | Detach (odłącz się od sesji) |
| `Ctrl+g` → `o` → `w` | Session manager (lista sesji) |
| `Ctrl+g` → `o` → `c` | Configuration plugin |
| `Ctrl+g` → `o` → `p` | Plugin manager |

### Move Mode (z normal: `m`)
Przenoszenie paneli:

| Pełny Skrót | Akcja |
|-------|-------|
| `Ctrl+g` → `m` → `n` | Przenieś panel (next) |
| `Ctrl+g` → `m` → `p` | Przenieś panel wstecz |
| `Ctrl+g` → `m` → `h/j/k/l` | Przenieś panel w kierunku |
| `Ctrl+g` → `m` → `strzałki` | Przenieś panel w kierunku |
| `Ctrl+g` → `m` → `Tab` | Przenieś panel |

## Sesje (Sessions)

### Tworzenie i Łączenie
```bash
# Nowa sesja z nazwą
zellij -s nazwa-sesji

# Nowa sesja z layoutem
zellij --layout nazwa-layoutu

# Lista sesji
zellij list-sessions

# Podłącz do sesji
zellij attach nazwa-sesji

# Podłącz do ostatniej
zellij attach

# Usuń sesję
zellij delete-session nazwa-sesji

# Zabij wszystkie sesje
zellij delete-all-sessions
```

## Layouty

Layouty są w `~/.config/zellij/layouts/`

Przykładowy layout (`dev.kdl`):
```kdl
layout {
    pane split_direction="vertical" {
        pane
        pane split_direction="horizontal" {
            pane
            pane
        }
    }
}
```

Uruchom z layoutem:
```bash
zellij --layout dev
```

## Konfiguracja

Główny plik: `~/.config/zellij/config.kdl`

### Przydatne opcje
```kdl
// Wyłącz pasek myszy
mouse_mode false

// Zmień domyślny shell
default_shell "fish"

// Kopiuj do schowka systemowego
copy_command "xclip -selection clipboard"

// Automatyczne przypinanie
auto_layout true
```

## Floating Panes (Pływające Panele)

| Skrót | Akcja |
|-------|-------|
| `Alt+f` | Toggle floating panes (najszybsze!) ⭐ |
| `Ctrl+g` → `p` → `w` | Toggle floating pane |
| `Ctrl+g` → `p` → `e` | Toggle embedded floating pane |

Floating panes to panele "unoszące się" nad innymi - przydatne do szybkich notatek, kalkulatora itp.

## Tips & Tricks (Omakub Edition)

### 1. ⭐ Używaj skrótów Alt!
To najważniejsza rada - **używaj `Alt`** zamiast wchodzenia w tryby:
- `Alt+h/j/k/l` - nawigacja (zamiast `Ctrl+g` → `p` → `h/j/k/l`)
- `Alt+n` - nowy panel (zamiast `Ctrl+g` → `p` → `n`)
- `Alt+f` - floating panes (zamiast `Ctrl+g` → `p` → `w`)
- `Alt++/-` - resize (zamiast wchodzenia w resize mode)

### 2. Locked mode to domyślny tryb
- Zellij startuje w **locked mode** - to normalne!
- Większość skrótów nie działa - to celowe (żeby nie kolidowały z programami)
- `Ctrl+g` odblokuje gdy potrzebujesz zaawansowanych funkcji
- Po akcji automatycznie wraca do locked mode

### 3. Fullscreen dla focus
`Ctrl+g` → `p` → `f` - schowaj inne panele i skup się na jednym

### 4. Kopiowanie z Zellij
Tekst zaznaczony myszką w Scroll Mode (`Ctrl+g` → `s`) automatycznie trafia do schowka systemowego

### 5. Sesje nazwane
Zawsze używaj nazw dla sesji roboczych:
```bash
zellij -s projekt-backend
zellij -s projekt-frontend
```

### 6. Session manager
`Ctrl+g` → `o` → `w` pokazuje wszystkie sesje - możesz szybko przełączać się między projektami

### 7. Edycja scrollback
`Ctrl+g` → `s` → `e` otwiera cały scrollback w nvim - świetne do kopiowania długich outputów

### 8. Layouty dla projektów
Stwórz layout dla każdego projektu z typową konfiguracją paneli (compact to default w Omakub)

## Porównanie z tmux

| Funkcja | Zellij (Omakub) | tmux |
|---------|--------|------|
| Unlock/Prefix | `Ctrl+g` (locked↔normal) | `Ctrl+b` |
| Nawigacja | `Alt+h/j/k/l` ⭐ | `Ctrl+b` → strzałki |
| Split w pionie | `Ctrl+g` → `p` → `r` | `Ctrl+b` → `%` |
| Split w poziomie | `Ctrl+g` → `p` → `d` | `Ctrl+b` → `"` |
| Nowy panel szybki | `Alt+n` ⭐ | brak |
| Nowy tab | `Ctrl+g` → `t` → `n` | `Ctrl+b` → `c` |
| Detach | `Ctrl+g` → `o` → `d` | `Ctrl+b` → `d` |
| Scroll | `Ctrl+g` → `s` | `Ctrl+b` → `[` |
| Resize | `Alt++/-` ⭐ | `Ctrl+b` → `:resize-pane` |
| Fullscreen | `Ctrl+g` → `p` → `f` | `Ctrl+b` → `z` |

**Główna różnica:** Omakub używa "locked by default" + skróty `Alt` dla częstych akcji!

## Najczęstsze Problemy

### Zellij nie startuje
```bash
# Sprawdź logi
zellij --debug

# Wyczyść cache
rm -rf ~/.cache/zellij
```

### Kopiowanie nie działa
Ustaw w `config.kdl`:
```kdl
copy_command "xclip -selection clipboard"
```

### Czcionka się sypie
Zainstaluj Nerd Font i ustaw w terminalu

## Przydatne Komendy

```bash
# Pokaż wersję
zellij --version

# Uruchom komendę w nowym panelu
zellij run -- htop

# Uruchom w tle (bez attachowania)
zellij -s background-task run -- long-running-command

# Setup completion (bash)
zellij setup --generate-completion bash > /etc/bash_completion.d/zellij
```

## Zasoby

- Dokumentacja: https://zellij.dev/documentation
- Repo: https://github.com/zellij-org/zellij
- Layouty społeczności: https://github.com/zellij-org/zellij/discussions

---

## Szybki Start (Omakub)

**Najprostszy workflow:**
1. `zellij` - uruchom (startujesz w locked mode)
2. `Alt+n` - nowy panel ⭐
3. `Alt+h/j/k/l` - poruszaj się między panelami ⭐
4. `Alt++/-` - zmień rozmiary ⭐
5. `Alt+f` - floating panel ⭐

**Zaawansowane funkcje:**
1. `Ctrl+g` - odblokuj (przejdź do normal mode)
2. `p` → `d` - podziel panel w dół
3. `p` → `r` - podziel panel w prawo
4. `p` → `f` - fullscreen
5. `t` → `n` - nowy tab
6. `o` → `d` - detach z sesji
7. `Esc` lub `Enter` - wróć do locked mode

**Zapamiętaj:**
- 🔒 **Locked mode** = domyślny, większość skrótów wyłączona
- ⌨️ **Alt+...** = działają zawsze, nawet w locked mode
- 🔓 **Ctrl+g** = przełącz locked ↔ normal
- ✅ Po akcji automatycznie wraca do locked mode
