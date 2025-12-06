# Omakub Web Apps - Instrukcja

Omakub umożliwia łatwe tworzenie webappów (Progressive Web Apps) które działają jak zwykłe aplikacje desktopowe.

## Szybki Start

### Stwórz webapp (podstawowe)

```bash
web2app 'Nazwa Aplikacji' https://adres-strony.com
```

### Stwórz webapp z własną ikoną

```bash
web2app 'Nazwa Aplikacji' https://adres-strony.com https://link-do-ikony.png
```

## Przykłady Gotowych Webappów

```bash
# YouTube Music
web2app 'YouTube Music' https://music.youtube.com

# Gmail
web2app 'Gmail' https://mail.google.com

# ChatGPT
web2app 'ChatGPT' https://chat.openai.com

# Google Photos
web2app 'Google Photos' https://photos.google.com

# GitHub
web2app 'GitHub' https://github.com

# Notion
web2app 'Notion' https://notion.so

# Figma
web2app 'Figma' https://figma.com

# Linear
web2app 'Linear' https://linear.app

# Spotify Web
web2app 'Spotify' https://open.spotify.com

# Discord Web
web2app 'Discord' https://discord.com/app
```

## Preinstalowane Web Apps

Omakub domyślnie instaluje:

1. **WhatsApp** - Komunikator
2. **HEY** - Email i kalendarz (37signals)
3. **Basecamp** - Zarządzanie projektami (37signals)

## Zarządzanie Webappami

### Instalacja z menu Omakub

```bash
omakub
# Wybierz: Install > Web Apps
```

### Usuwanie webapp

```bash
web2app-remove 'Nazwa Aplikacji'
```

### Lokalizacja plików

Wszystkie webappy są przechowywane jako pliki `.desktop` w:

```bash
~/.local/share/applications/
```

### Sprawdź zainstalowane webappy

```bash
ls ~/.local/share/applications/*.desktop
```

### Edycja webapp

```bash
# Lista webappów
ls ~/.local/share/applications/

# Edytuj plik .desktop
nvim ~/.local/share/applications/nazwa-aplikacji.desktop
```

## Ikony dla Webappów

### Źródła ikon

1. **Dashboard Icons** - https://dashboardicons.com/
2. **Simple Icons** - https://simpleicons.org/
3. **IconFinder** - https://iconfinder.com/
4. **Oficjalne strony** - Wiele stron ma ikony w formacie PNG/SVG

### Format ikon

- **Zalecany:** PNG lub SVG
- **Rozmiar:** 256x256px lub większy
- **URL:** Bezpośredni link do pliku obrazu

### Przykład z własną ikoną

```bash
web2app 'Slack' https://app.slack.com https://cdn.worldvectorlogo.com/logos/slack-new-logo.svg
```

## Tworzenie Własnego Webapp

### Krok po kroku

1. **Znajdź stronę** którą chcesz jako app
2. **Znajdź ikonę** (opcjonalnie)
3. **Uruchom komendę:**
   ```bash
   web2app 'Moja Aplikacja' https://example.com [url-ikony]
   ```
4. **Otwórz launcher** (`Super+Space`)
5. **Wpisz nazwę** swojej aplikacji
6. **Gotowe!**

### Przykład: Tworzenie webapp dla Excalidraw

```bash
web2app 'Excalidraw' https://excalidraw.com
```

## Zaawansowane Użycie

### Ręczne tworzenie pliku .desktop

Jeśli potrzebujesz większej kontroli, możesz stworzyć plik `.desktop` ręcznie:

```bash
nvim ~/.local/share/applications/moja-aplikacja.desktop
```

**Zawartość pliku:**

```desktop
[Desktop Entry]
Name=Moja Aplikacja
Exec=google-chrome --app=https://example.com
Icon=/path/to/icon.png
Type=Application
Categories=Network;WebBrowser;
Terminal=false
StartupWMClass=example.com
```

### Zmień przeglądarkę

Domyślnie używany jest Google Chrome. Możesz zmienić na inną:

```bash
# Chromium
Exec=chromium --app=https://example.com

# Firefox
Exec=firefox --new-window https://example.com

# Brave
Exec=brave --app=https://example.com
```

## Workflow z Webappami

### Organizacja workspace

```bash
# Workspace 1: Komunikacja
# - Slack webapp
# - Discord webapp
# - WhatsApp webapp

# Workspace 2: Praca
# - GitHub webapp
# - Linear webapp
# - Figma webapp

# Workspace 3: Rozrywka
# - YouTube Music webapp
# - Spotify webapp
```

### Ulauncher integration

Webappy pojawiają się automatycznie w Ulauncher:

```bash
Super+Space
wpisz: nazwa webapp
Enter
```

### Skróty klawiszowe

Możesz dodać skróty do uruchamiania webappów w ustawieniach systemu:

1. Otwórz Settings → Keyboard → Shortcuts
2. Dodaj Custom Shortcut
3. Command: `gtk-launch nazwa-pliku.desktop`
4. Przypisz skrót (np. `Super+Shift+G` dla Gmail)

## Troubleshooting

### Webapp się nie uruchamia

```bash
# Sprawdź czy plik istnieje
ls ~/.local/share/applications/ | grep nazwa

# Sprawdź zawartość
cat ~/.local/share/applications/nazwa.desktop

# Sprawdź uprawnienia
chmod +x ~/.local/share/applications/nazwa.desktop

# Odśwież cache
update-desktop-database ~/.local/share/applications/
```

### Ikona się nie wyświetla

```bash
# Sprawdź czy URL ikony działa
wget [url-ikony] -O /tmp/test-icon.png

# Użyj lokalnej ikony zamiast URL
# Pobierz ikonę:
wget [url-ikony] -O ~/.local/share/icons/moja-ikona.png

# Edytuj .desktop i zmień Icon na:
Icon=/home/username/.local/share/icons/moja-ikona.png
```

### Webapp nie pojawia się w launcherze

```bash
# Odśwież bazę aplikacji
update-desktop-database ~/.local/share/applications/

# Restart Ulauncher
pkill ulauncher && ulauncher &
```

### Usunięcie wszystkich webappów

```bash
# Lista wszystkich
ls ~/.local/share/applications/*.desktop

# Usuń wybrane
rm ~/.local/share/applications/nazwa.desktop

# OSTROŻNIE: Usuń wszystkie (backup first!)
rm ~/.local/share/applications/*.desktop
```

## Tips & Tricks

### 1. Grupowanie podobnych stron

```bash
# Stwórz osobne webappy dla różnych kont
web2app 'Gmail Personal' https://mail.google.com
web2app 'Gmail Work' https://mail.google.com

# Każdy otworzy się jako osobne okno
```

### 2. PWA z notyfikacjami

Niektóre strony wspierają notyfikacje desktop - po pierwszym uruchomieniu webapp zapyta o pozwolenie.

### 3. Tryb kiosk

```bash
# Pełny ekran bez żadnych kontrolek
Exec=google-chrome --app=https://example.com --kiosk
```

### 4. Backup webappów

```bash
# Backup wszystkich webappów
cp ~/.local/share/applications/*.desktop ~/backup-webapps/

# Restore
cp ~/backup-webapps/*.desktop ~/.local/share/applications/
```

### 5. Share webappy między użytkownikami

```bash
# Zainstaluj systemowo (wymaga sudo)
sudo cp webapp.desktop /usr/share/applications/
```

## Popularne Webappy dla Developerów

```bash
# Development
web2app 'GitHub' https://github.com
web2app 'GitLab' https://gitlab.com
web2app 'Vercel' https://vercel.com/dashboard
web2app 'Railway' https://railway.app
web2app 'Netlify' https://app.netlify.com

# Design
web2app 'Figma' https://figma.com
web2app 'Excalidraw' https://excalidraw.com
web2app 'Whimsical' https://whimsical.com

# Productivity
web2app 'Notion' https://notion.so
web2app 'Linear' https://linear.app
web2app 'Todoist' https://todoist.com/app

# Communication
web2app 'Slack' https://app.slack.com
web2app 'Discord' https://discord.com/app
web2app 'Telegram Web' https://web.telegram.org

# AI Tools
web2app 'ChatGPT' https://chat.openai.com
web2app 'Claude' https://claude.ai
web2app 'Perplexity' https://perplexity.ai

# Cloud Storage
web2app 'Google Drive' https://drive.google.com
web2app 'Dropbox' https://dropbox.com
```

## Zasoby

- **Omakub Docs:** https://omakub.org/
- **Web Apps Manual:** https://learn.omacom.io/1/read/46/web-apps
- **Dashboard Icons:** https://dashboardicons.com/
- **Simple Icons:** https://simpleicons.org/

---

## Quick Reference

```bash
# Stwórz webapp
web2app 'Nazwa' https://url.com

# Stwórz webapp z ikoną
web2app 'Nazwa' https://url.com https://icon-url.png

# Usuń webapp
web2app-remove 'Nazwa'

# Menu instalacji
omakub

# Sprawdź webappy
ls ~/.local/share/applications/

# Odśwież launcher
update-desktop-database ~/.local/share/applications/
```

**Enjoy your webapps! 🚀**
