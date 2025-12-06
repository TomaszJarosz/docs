# Modifier Key Remapping Fix

## Problem
Key remapping was not working automatically after system startup, despite having xmodmap configuration and autostart configured.

## Mapping Goals
- **Left Alt** → Left Control
- **Left Windows (Super)** → Left Alt
- **Left Control** → Left Windows (Super)

## Diagnosis
- System: Ubuntu with Omakub, X11
- Configuration files were correct:
  - `~/.Xmodmap` - contained valid remapping configuration
  - `~/.config/autostart/xmodmap-keys.desktop` - autostart file existed
- Problem: GNOME was resetting xmodmap settings before they were fully applied

## Solution

### Configuration file: `~/.Xmodmap`
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

### Fixed autostart: `~/.config/autostart/xmodmap-keys.desktop`
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

**Key change:** Added `sleep 3` to give GNOME time to fully initialize before applying xmodmap.

## Manual Mapping Application

### Quick way (alias)
```bash
fixkeys
```

### Full command
```bash
xmodmap ~/.Xmodmap
```

**The `fixkeys` alias** is defined in `~/.bashrc` and is the fastest way to restore the mapping after screen unlock.

## Verification
Check current mapping:
```bash
xmodmap -pke | grep -E "keycode (37|64|133) ="
```

Should display:
- `keycode 37 = Super_L NoSymbol Super_L`
- `keycode 64 = Control_L NoSymbol Control_L`
- `keycode 133 = Alt_L Meta_L Alt_L Meta_L`

## If it still doesn't work
If mapping still doesn't work after restart:

1. **Increase the delay** in the autostart file to 5-7 seconds:
   ```
   Exec=sh -c "sleep 7 && xmodmap /home/tomasz/.Xmodmap"
   ```

2. **Check system logs** to see if autostart is running:
   ```bash
   journalctl --user -b | grep -i xmodmap
   ```

3. **Alternatively** add mapping to `~/.profile` or `~/.bashrc` (though it will only work in terminals)

---
Fix date: 2025-11-15
