# Omakub Web Apps - Guide

Omakub enables easy creation of webapps (Progressive Web Apps) that work like regular desktop applications.

## Quick Start

### Create webapp (basic)

```bash
web2app 'App Name' https://website-address.com
```

### Create webapp with custom icon

```bash
web2app 'App Name' https://website-address.com https://icon-link.png
```

## Ready-Made Webapp Examples

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

## Pre-installed Web Apps

Omakub installs by default:

1. **WhatsApp** - Messenger
2. **HEY** - Email and calendar (37signals)
3. **Basecamp** - Project management (37signals)

## Managing Webapps

### Installation from Omakub menu

```bash
omakub
# Select: Install > Web Apps
```

### Removing webapp

```bash
web2app-remove 'App Name'
```

### File locations

All webapps are stored as `.desktop` files in:

```bash
~/.local/share/applications/
```

### Check installed webapps

```bash
ls ~/.local/share/applications/*.desktop
```

### Editing webapp

```bash
# List webapps
ls ~/.local/share/applications/

# Edit .desktop file
nvim ~/.local/share/applications/app-name.desktop
```

## Icons for Webapps

### Icon sources

1. **Dashboard Icons** - https://dashboardicons.com/
2. **Simple Icons** - https://simpleicons.org/
3. **IconFinder** - https://iconfinder.com/
4. **Official websites** - Many sites have icons in PNG/SVG format

### Icon format

- **Recommended:** PNG or SVG
- **Size:** 256x256px or larger
- **URL:** Direct link to image file

### Example with custom icon

```bash
web2app 'Slack' https://app.slack.com https://cdn.worldvectorlogo.com/logos/slack-new-logo.svg
```

## Creating Your Own Webapp

### Step by step

1. **Find the website** you want as an app
2. **Find an icon** (optional)
3. **Run the command:**
   ```bash
   web2app 'My Application' https://example.com [icon-url]
   ```
4. **Open launcher** (`Super+Space`)
5. **Type the name** of your application
6. **Done!**

### Example: Creating webapp for Excalidraw

```bash
web2app 'Excalidraw' https://excalidraw.com
```

## Advanced Usage

### Manual creation of .desktop file

If you need more control, you can create a `.desktop` file manually:

```bash
nvim ~/.local/share/applications/my-app.desktop
```

**File contents:**

```desktop
[Desktop Entry]
Name=My Application
Exec=google-chrome --app=https://example.com
Icon=/path/to/icon.png
Type=Application
Categories=Network;WebBrowser;
Terminal=false
StartupWMClass=example.com
```

### Change browser

Google Chrome is used by default. You can change to another:

```bash
# Chromium
Exec=chromium --app=https://example.com

# Firefox
Exec=firefox --new-window https://example.com

# Brave
Exec=brave --app=https://example.com
```

## Workflow with Webapps

### Workspace organization

```bash
# Workspace 1: Communication
# - Slack webapp
# - Discord webapp
# - WhatsApp webapp

# Workspace 2: Work
# - GitHub webapp
# - Linear webapp
# - Figma webapp

# Workspace 3: Entertainment
# - YouTube Music webapp
# - Spotify webapp
```

### Ulauncher integration

Webapps appear automatically in Ulauncher:

```bash
Super+Space
type: webapp name
Enter
```

### Keyboard shortcuts

You can add shortcuts to launch webapps in system settings:

1. Open Settings → Keyboard → Shortcuts
2. Add Custom Shortcut
3. Command: `gtk-launch filename.desktop`
4. Assign shortcut (e.g. `Super+Shift+G` for Gmail)

## Troubleshooting

### Webapp doesn't launch

```bash
# Check if file exists
ls ~/.local/share/applications/ | grep name

# Check contents
cat ~/.local/share/applications/name.desktop

# Check permissions
chmod +x ~/.local/share/applications/name.desktop

# Refresh cache
update-desktop-database ~/.local/share/applications/
```

### Icon doesn't display

```bash
# Check if icon URL works
wget [icon-url] -O /tmp/test-icon.png

# Use local icon instead of URL
# Download icon:
wget [icon-url] -O ~/.local/share/icons/my-icon.png

# Edit .desktop and change Icon to:
Icon=/home/username/.local/share/icons/my-icon.png
```

### Webapp doesn't appear in launcher

```bash
# Refresh application database
update-desktop-database ~/.local/share/applications/

# Restart Ulauncher
pkill ulauncher && ulauncher &
```

### Removing all webapps

```bash
# List all
ls ~/.local/share/applications/*.desktop

# Remove selected
rm ~/.local/share/applications/name.desktop

# CAREFUL: Remove all (backup first!)
rm ~/.local/share/applications/*.desktop
```

## Tips & Tricks

### 1. Grouping similar pages

```bash
# Create separate webapps for different accounts
web2app 'Gmail Personal' https://mail.google.com
web2app 'Gmail Work' https://mail.google.com

# Each will open as a separate window
```

### 2. PWA with notifications

Some websites support desktop notifications - after first launch webapp will ask for permission.

### 3. Kiosk mode

```bash
# Full screen without any controls
Exec=google-chrome --app=https://example.com --kiosk
```

### 4. Backup webapps

```bash
# Backup all webapps
cp ~/.local/share/applications/*.desktop ~/backup-webapps/

# Restore
cp ~/backup-webapps/*.desktop ~/.local/share/applications/
```

### 5. Share webapps between users

```bash
# Install system-wide (requires sudo)
sudo cp webapp.desktop /usr/share/applications/
```

## Popular Webapps for Developers

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

## Resources

- **Omakub Docs:** https://omakub.org/
- **Web Apps Manual:** https://learn.omacom.io/1/read/46/web-apps
- **Dashboard Icons:** https://dashboardicons.com/
- **Simple Icons:** https://simpleicons.org/

---

## Quick Reference

```bash
# Create webapp
web2app 'Name' https://url.com

# Create webapp with icon
web2app 'Name' https://url.com https://icon-url.png

# Remove webapp
web2app-remove 'Name'

# Installation menu
omakub

# Check webapps
ls ~/.local/share/applications/

# Refresh launcher
update-desktop-database ~/.local/share/applications/
```

**Enjoy your webapps! 🚀**
