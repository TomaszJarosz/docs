# Naprawa mapowania klawiszy modyfikujących

## Problem
Mapowanie klawiszy nie działało automatycznie po uruchomieniu systemu, mimo że była skonfigurowana konfiguracja xmodmap i autostart.

## Cel mapowania
- **Lewy Alt** → Lewy Control
- **Lewy Windows (Super)** → Lewy Alt
- **Lewy Control** → Lewy Windows (Super)

## Diagnoza
- System: Ubuntu z Omakub, X11
- Pliki konfiguracyjne były poprawne:
  - `~/.Xmodmap` - zawierał prawidłową konfigurację remapowania
  - `~/.config/autostart/xmodmap-keys.desktop` - plik autostartu istniał
- Problem: GNOME resetował ustawienia xmodmap zanim zostały w pełni zastosowane

## Rozwiązanie

### Plik konfiguracyjny: `~/.Xmodmap`
```
! Remapping left modifier keys:
! Left Alt -> Left Control
! Left Super (Windows) -> Left Alt
! Left Control -> Left Super

! First, clear the modifier mappings
clear control
clear mod1
clear mod4

! Remap the keycodes to new keysyms
keycode 64 = Control_L NoSymbol Control_L
keycode 133 = Alt_L Meta_L Alt_L Meta_L
keycode 37 = Super_L NoSymbol Super_L

! Rebuild the modifier mappings
add control = Control_L Control_R
add mod1 = Alt_L Meta_L
add mod4 = Super_L Super_R
```

### Poprawiony autostart: `~/.config/autostart/xmodmap-keys.desktop`
```
[Desktop Entry]
Type=Application
Name=Keyboard Remapping
Comment=Remap left modifier keys (Alt->Ctrl, Win->Alt, Ctrl->Win)
Exec=sh -c "sleep 3 && xmodmap /home/tomasz/.Xmodmap"
Terminal=false
StartupNotify=false
X-GNOME-Autostart-enabled=true
```

**Kluczowa zmiana:** Dodano `sleep 3` aby dać GNOME czas na pełną inicjalizację przed zastosowaniem xmodmap.

## Ręczne zastosowanie mapowania

### Szybki sposób (alias)
```bash
fixkeys
```

### Pełna komenda
```bash
xmodmap ~/.Xmodmap
```

**Alias `fixkeys`** jest zdefiniowany w `~/.bashrc` i jest najszybszym sposobem na przywrócenie mapowania po odblokowaniu ekranu.

## Weryfikacja
Sprawdź aktualne mapowanie:
```bash
xmodmap -pke | grep -E "keycode (37|64|133) ="
```

Powinno pokazać:
- `keycode 37 = Super_L NoSymbol Super_L`
- `keycode 64 = Control_L NoSymbol Control_L`
- `keycode 133 = Alt_L Meta_L Alt_L Meta_L`

## Jeśli nadal nie działa
Jeśli po restarcie mapowanie nadal nie działa:

1. **Zwiększ opóźnienie** w pliku autostartu do 5-7 sekund:
   ```
   Exec=sh -c "sleep 7 && xmodmap /home/tomasz/.Xmodmap"
   ```

2. **Sprawdź logi systemowe** aby zobaczyć czy autostart się uruchamia:
   ```bash
   journalctl --user -b | grep -i xmodmap
   ```

3. **Alternatywnie** dodaj mapowanie do `~/.profile` lub `~/.bashrc` (choć będzie działać tylko w terminalach)

---
Data naprawy: 2025-11-15
