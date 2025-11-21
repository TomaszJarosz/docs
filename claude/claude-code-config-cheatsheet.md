# Claude Code - Konfiguracja i Cheatsheet

Kompletny przewodnik po konfigurowaniu i używaniu Claude Code.

## Podstawowe Informacje

**Claude Code** to oficjalny CLI tool od Anthropic dla interakcji z Claude w terminalu.

- 🌐 **Oficjalna strona:** https://code.claude.com/
- 📚 **Dokumentacja:** https://code.claude.com/docs
- 🐙 **GitHub:** https://github.com/anthropics/claude-code

## Instalacja i Pierwsze Kroki

### Instalacja

```bash
# Instalacja (zazwyczaj przez npm)
npm install -g claude-code

# Lub przez oficjalny installer
curl -fsSL https://code.claude.com/install.sh | sh

# Sprawdź wersję
claude --version
```

### Pierwsze Uruchomienie

```bash
# Uruchom Claude Code
claude

# Lub w konkretnym katalogu
cd ~/projekt
claude

# Z konkretnym plikiem
claude file.py
```

### Konfiguracja API Key

```bash
# Claude Code automatycznie poprosi o API key przy pierwszym uruchomieniu
# Lub ustaw ręcznie:
export ANTHROPIC_API_KEY="your-api-key-here"

# Dodaj do ~/.bashrc lub ~/.zshrc:
echo 'export ANTHROPIC_API_KEY="your-key"' >> ~/.bashrc
```

## Struktura Konfiguracji

### Lokalizacje Plików

```
~/.config/claude-code/          # Główny folder konfiguracji
├── settings.json               # Ustawienia globalne
├── .env                        # Zmienne środowiskowe
└── cache/                      # Cache

.claude/                        # Folder projektu (w repo)
├── commands/                   # Slash commands
│   ├── command1.md
│   └── command2.md
├── settings.json               # Ustawienia projektu
└── prompts/                    # Własne prompty
```

## settings.json - Konfiguracja

### Lokalizacja

```bash
# Globalna konfiguracja
~/.config/claude-code/settings.json

# Konfiguracja projektu (w repo)
.claude/settings.json
```

### Przykładowa Konfiguracja Globalna

```json
{
  "model": "claude-sonnet-4-5",
  "apiKey": "${ANTHROPIC_API_KEY}",

  "autoApproveTools": {
    "Read": [
      "//home/tomasz/**",
      "//**/docs/**",
      "//**/*.md"
    ],
    "Grep": [
      "//home/tomasz/**"
    ],
    "Glob": [
      "//home/tomasz/**"
    ],
    "Bash": {
      "tar:*": true,
      "git status": true,
      "git diff": true,
      "ls*": true,
      "cat*": true
    }
  },

  "customInstructions": "Zawsze odpowiadaj po polsku. Używaj konkretnych przykładów.",

  "theme": "dark",

  "statusLine": {
    "enabled": true,
    "format": "{{model}} | {{tokens}}"
  },

  "gitignore": [
    "node_modules/",
    ".env",
    "*.log",
    ".cache/"
  ],

  "maxTokens": 200000,

  "temperature": 1.0,

  "hooks": {
    "preToolCall": null,
    "postToolCall": null,
    "userPromptSubmit": null
  }
}
```

### Przykładowa Konfiguracja Projektu

```json
{
  "customInstructions": "To jest projekt React. Używaj TypeScript i functional components.",

  "autoApproveTools": {
    "Read": ["//**/*.ts", "//**/*.tsx", "//**/*.json"],
    "Bash": {
      "npm *": true,
      "yarn *": true
    }
  },

  "gitignore": [
    "node_modules/",
    "dist/",
    "build/"
  ]
}
```

## Uprawnienia (autoApproveTools)

### Dozwolone Ścieżki dla Read/Grep/Glob

```json
{
  "autoApproveTools": {
    "Read": [
      "//home/tomasz/**",           // Cały home directory
      "//**/src/**",                 // Wszystkie foldery src
      "//**/*.{js,ts,py}",          // Konkretne rozszerzenia
      "//home/tomasz/projekt/**"    // Konkretny projekt
    ],
    "Grep": [
      "//home/tomasz/projekty/**"
    ],
    "Glob": [
      "//home/tomasz/**"
    ]
  }
}
```

**Pattern syntax:**
- `//` - absolute path
- `*` - dowolne znaki (nie /)
- `**` - dowolne znaki (including /)
- `{js,ts}` - alternatywy
- `[0-9]` - character class

### Dozwolone Komendy Bash

```json
{
  "autoApproveTools": {
    "Bash": {
      // Proste komendy
      "ls": true,
      "pwd": true,
      "date": true,

      // Z argumentami (wildcard)
      "git status": true,
      "git diff*": true,
      "npm *": true,
      "ls *": true,

      // Tar operations
      "tar:*": true,

      // Pattern matching
      "echo*": true,
      "cat *": true
    }
  }
}
```

**Uwaga:** Bądź ostrożny z wildcardami! `"rm*": true` byłoby niebezpieczne.

### Zalecane Ustawienia Bezpieczeństwa

```json
{
  "autoApproveTools": {
    "Read": ["//home/tomasz/**"],
    "Grep": ["//home/tomasz/**"],
    "Glob": ["//home/tomasz/**"],
    "Bash": {
      // Bezpieczne komendy tylko do odczytu
      "ls*": true,
      "cat*": true,
      "head*": true,
      "tail*": true,
      "git status": true,
      "git diff*": true,
      "git log*": true,
      "pwd": true,
      "date": true,
      "whoami": true,
      "uname*": true,

      // Build tools (zazwyczaj bezpieczne)
      "npm test": true,
      "npm run build": true,
      "cargo build": true,
      "make": true
    }
  }
}
```

**NIE dodawaj:**
- `rm*` - usuwanie plików
- `sudo*` - komendy z sudo
- `dd*` - niebezpieczne operacje na dysku
- `mkfs*` - formatowanie
- Dowolne destructive commands

## Slash Commands (Własne Komendy)

### Tworzenie Slash Command

```bash
# Utwórz folder dla komend
mkdir -p .claude/commands

# Utwórz komendę
nvim .claude/commands/review.md
```

**Przykład: `.claude/commands/review.md`**
```markdown
---
description: Code review tego pliku
---

Przejrzyj ten plik i znajdź:
1. Potencjalne bugi
2. Problemy z wydajnością
3. Naruszenia best practices
4. Sugestie ulepszeń

Sformatuj jako:
- 🐛 Bug: opis
- ⚡ Performance: opis
- 📖 Best Practice: opis
- 💡 Suggestion: opis
```

### Użycie

```bash
# W Claude Code:
/review path/to/file.js
```

### Przykładowe Slash Commands

**`.claude/commands/test.md`**
```markdown
---
description: Napisz testy dla tego kodu
---

Napisz kompletne unit testy dla {{file}}.
Użyj frameworka testowego odpowiedniego dla języka.
Pokryj edge cases i error handling.
```

**`.claude/commands/doc.md`**
```markdown
---
description: Generuj dokumentację
---

Wygeneruj pełną dokumentację dla {{file}}:
- Opis funkcji/klas
- Parametry i zwracane wartości
- Przykłady użycia
- Edge cases

Format: JSDoc / docstrings / rustdoc (zależnie od języka)
```

**`.claude/commands/optimize.md`**
```markdown
---
description: Optymalizuj kod
---

Zoptymalizuj ten kod pod kątem:
1. Wydajności
2. Czytelności
3. Memory usage
4. Best practices

Wyjaśnij każdą zmianę.
```

**`.claude/commands/translate.md`**
```markdown
---
description: Przetłumacz kod na inny język
---

Przetłumacz {{file}} na {{language}}.
Zachowaj:
- Funkcjonalność
- Strukturę
- Komentarze
- Error handling

Dodaj komentarze o różnicach między językami.
```

### Parametry w Slash Commands

```markdown
<!-- Użycie zmiennych -->
{{file}}        - aktualny plik
{{language}}    - przekazany parametr
{{selection}}   - zaznaczony tekst
{{arg1}}        - argument 1
{{arg2}}        - argument 2

<!-- Przykład użycia: -->
/translate rust

<!-- W markdown: -->
Przetłumacz na {{language}}.
```

## Hooks - Automatyzacja

Hooks pozwalają uruchamiać skrypty w odpowiedzi na eventy.

### Typy Hooków

1. **userPromptSubmit** - przed wysłaniem promptu
2. **preToolCall** - przed użyciem narzędzia
3. **postToolCall** - po użyciu narzędzia

### Konfiguracja w settings.json

```json
{
  "hooks": {
    "userPromptSubmit": "~/.claude/hooks/pre-submit.sh",
    "preToolCall": "~/.claude/hooks/pre-tool.sh",
    "postToolCall": "~/.claude/hooks/post-tool.sh"
  }
}
```

### Przykładowy Hook: Pre-Commit Check

**`~/.claude/hooks/pre-tool.sh`**
```bash
#!/bin/bash

# Jeśli Claude chce użyć git commit, najpierw uruchom testy
if [[ "$TOOL_NAME" == "Bash" ]] && [[ "$TOOL_ARGS" == *"git commit"* ]]; then
    echo "🧪 Uruchamiam testy przed commitem..."
    npm test || exit 1
fi

# Jeśli wszystko OK, pozwól
exit 0
```

### Przykładowy Hook: Auto-format

**`~/.claude/hooks/post-tool.sh`**
```bash
#!/bin/bash

# Po edycji pliku, auto-format
if [[ "$TOOL_NAME" == "Edit" ]] || [[ "$TOOL_NAME" == "Write" ]]; then
    FILE="$TOOL_RESULT_FILE"

    if [[ $FILE == *.js ]] || [[ $FILE == *.ts ]]; then
        prettier --write "$FILE"
    elif [[ $FILE == *.py ]]; then
        black "$FILE"
    elif [[ $FILE == *.rs ]]; then
        rustfmt "$FILE"
    fi
fi
```

### Przykładowy Hook: Linting

**`~/.claude/hooks/pre-submit.sh`**
```bash
#!/bin/bash

# Przed każdym promptem, sprawdź czy repo jest clean
if git status --porcelain | grep -q .; then
    echo "⚠️  Masz niezacommitowane zmiany!"
fi
```

**Pamiętaj:**
```bash
# Zrób hooki wykonywalne
chmod +x ~/.claude/hooks/*.sh
```

## MCP Servers (Model Context Protocol)

MCP pozwala Claude Code na integrację z zewnętrznymi narzędziami.

### Konfiguracja MCP

**`~/.config/claude-code/mcp-servers.json`**
```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/home/tomasz/projekty"]
    },
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_TOKEN": "${GITHUB_TOKEN}"
      }
    },
    "postgres": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-postgres"],
      "env": {
        "DATABASE_URL": "${DATABASE_URL}"
      }
    }
  }
}
```

### Dostępne MCP Servers

```bash
# Filesystem access
@modelcontextprotocol/server-filesystem

# GitHub integration
@modelcontextprotocol/server-github

# PostgreSQL
@modelcontextprotocol/server-postgres

# Slack
@modelcontextprotocol/server-slack

# Google Drive
@modelcontextprotocol/server-gdrive

# Brave Search
@modelcontextprotocol/server-brave-search

# Memory (długoterminowa pamięć)
@modelcontextprotocol/server-memory
```

### Własny MCP Server

**`my-mcp-server.js`**
```javascript
#!/usr/bin/env node

const { Server } = require('@modelcontextprotocol/sdk/server/index.js');
const { StdioServerTransport } = require('@modelcontextprotocol/sdk/server/stdio.js');

const server = new Server({
  name: 'my-custom-server',
  version: '1.0.0',
}, {
  capabilities: {
    tools: {},
  },
});

// Definicja narzędzia
server.setRequestHandler('tools/list', async () => {
  return {
    tools: [{
      name: 'get_weather',
      description: 'Pobierz pogodę dla miasta',
      inputSchema: {
        type: 'object',
        properties: {
          city: { type: 'string' }
        },
        required: ['city']
      }
    }]
  };
});

server.setRequestHandler('tools/call', async (request) => {
  if (request.params.name === 'get_weather') {
    // Implementacja
    return { content: [{ type: 'text', text: 'Sunny, 20°C' }] };
  }
});

const transport = new StdioServerTransport();
server.connect(transport);
```

## Custom Instructions (Systeminstrukcje)

### Globalne Custom Instructions

**`~/.config/claude-code/settings.json`**
```json
{
  "customInstructions": "1. Zawsze odpowiadaj po polsku\n2. Używaj konkretnych przykładów\n3. Dla kodu Python używaj type hints\n4. Commituj małe, atomowe zmiany"
}
```

### Per-Project Instructions

**`.claude/settings.json`**
```json
{
  "customInstructions": "To jest projekt e-commerce w Django.\n\nGuidelines:\n- Używaj Class-Based Views\n- Wszystkie API endpoints przez DRF\n- Testy w pytest\n- Dokumentacja w docstrings (Google style)\n- Pre-commit hooks: black, flake8, mypy"
}
```

### Advanced Custom Instructions

```json
{
  "customInstructions": "# Role\nJesteś ekspertem od Rust i performance.\n\n# Code Style\n- Używaj idiomatic Rust\n- Zawsze wykorzystuj type system\n- Error handling przez Result<T, E>\n- Dokumentacja z przykładami\n\n# Testing\n- Unit testy dla każdej funkcji\n- Integration testy dla modułów\n- Benchmarki dla performance-critical code\n\n# Commit Messages\nFormat: <type>(<scope>): <subject>\nTypes: feat, fix, docs, refactor, test, chore"
}
```

## .gitignore dla Claude Code

Dodaj do `.gitignore`:

```gitignore
# Claude Code cache
.claude/cache/
.claude/.cache/

# Nie ignoruj konfiguracji i komend
!.claude/settings.json
!.claude/commands/
!.claude/prompts/

# Ignoruj logi
.claude/*.log

# API keys (jeśli przypadkowo w projekcie)
.claude/.env
```

## Przydatne Komendy CLI

```bash
# Uruchom Claude w projekcie
claude

# Z konkretnym modelem
claude --model claude-opus-4

# Zobacz wersję
claude --version

# Pomoc
claude --help

# Reset cache
rm -rf ~/.config/claude-code/cache/

# Zobacz aktualną konfigurację
cat ~/.config/claude-code/settings.json

# Test slash command
# W Claude Code:
/command-name arg1 arg2
```

## Skróty Klawiszowe w Claude Code

| Skrót | Akcja |
|-------|-------|
| `Ctrl+C` | Przerwij generowanie odpowiedzi |
| `Ctrl+D` | Wyjdź z Claude Code |
| `↑/↓` | Historia promptów |
| `Tab` | Autocomplete (slash commands) |
| `/help` | Lista dostępnych slash commands |
| `/clear` | Wyczyść konwersację |

## Workflow Tips

### 1. Projekt Setup

```bash
# W nowym projekcie:
mkdir -p .claude/commands
cat > .claude/settings.json << 'EOF'
{
  "customInstructions": "Opis projektu...",
  "autoApproveTools": {
    "Read": ["//**"],
    "Bash": {
      "npm*": true,
      "git*": true
    }
  }
}
EOF

# Dodaj podstawowe komendy
echo "---\ndescription: Code review\n---\nPrzejrzyj kod..." > .claude/commands/review.md
```

### 2. Team Configuration

Udostępnij `.claude/` w repo:

```bash
git add .claude/
git commit -m "Add Claude Code configuration"
git push
```

Zespół ma teraz te same:
- Slash commands
- Custom instructions
- Auto-approve rules (jeśli bezpieczne)

### 3. Multi-Project Workflow

```bash
# Globalna konfiguracja dla wszystkich projektów
~/.config/claude-code/settings.json

# + per-project overrides
~/projekt1/.claude/settings.json
~/projekt2/.claude/settings.json
```

### 4. Environment Variables

**`.claude/.env`**
```bash
ANTHROPIC_API_KEY=sk-...
GITHUB_TOKEN=ghp_...
DATABASE_URL=postgresql://...
```

**Użycie w settings.json:**
```json
{
  "apiKey": "${ANTHROPIC_API_KEY}"
}
```

## Troubleshooting

### Claude nie widzi plików

```bash
# Sprawdź uprawnienia
ls -la .claude/

# Sprawdź settings.json
cat .claude/settings.json

# Dodaj do autoApproveTools
{
  "autoApproveTools": {
    "Read": ["//home/tomasz/**"]
  }
}
```

### Slash command nie działa

```bash
# Sprawdź czy plik istnieje
ls .claude/commands/

# Sprawdź format pliku (musi być .md)
# Sprawdź header:
---
description: Opis
---
```

### Hook nie wykonuje się

```bash
# Sprawdź permissions
chmod +x ~/.claude/hooks/*.sh

# Sprawdź czy ścieżka w settings.json jest poprawna
cat ~/.config/claude-code/settings.json | grep hooks

# Debug hook
bash -x ~/.claude/hooks/pre-tool.sh
```

### MCP server nie działa

```bash
# Sprawdź czy server jest zainstalowany
npx @modelcontextprotocol/server-filesystem --version

# Sprawdź logi
~/.config/claude-code/logs/mcp-*.log

# Test ręcznie
npx @modelcontextprotocol/server-filesystem /path/to/dir
```

## Best Practices

### 1. Bezpieczeństwo

```json
{
  "autoApproveTools": {
    // ✅ Dobre - tylko odczyt
    "Read": ["//home/tomasz/projekty/**"],
    "Grep": ["//home/tomasz/projekty/**"],

    // ❌ Złe - zbyt szerokie uprawnienia
    "Bash": { "*": true },

    // ✅ Dobre - konkretne komendy
    "Bash": {
      "git status": true,
      "npm test": true
    }
  }
}
```

### 2. Organization

```
.claude/
├── settings.json              # Konfiguracja projektu
├── commands/                  # Slash commands
│   ├── review.md
│   ├── test.md
│   └── doc.md
├── prompts/                   # Reusable prompts
│   └── code-style.md
└── .env                       # Secrets (w .gitignore!)
```

### 3. Documentation

Dokumentuj custom commands:

**`README.md`**
```markdown
## Claude Code Commands

- `/review` - Code review pliku
- `/test` - Generuj testy
- `/doc` - Generuj dokumentację
- `/optimize` - Optymalizuj kod
```

### 4. Team Sharing

```bash
# Commituj tylko bezpieczne rzeczy
git add .claude/settings.json
git add .claude/commands/

# NIE commituj
.claude/.env          # Secrets
.claude/cache/        # Cache
```

## Przykładowe Complete Setup

### ~/.config/claude-code/settings.json

```json
{
  "model": "claude-sonnet-4-5",
  "maxTokens": 200000,
  "temperature": 1.0,

  "autoApproveTools": {
    "Read": ["//home/tomasz/**"],
    "Grep": ["//home/tomasz/**"],
    "Glob": ["//home/tomasz/**"],
    "Bash": {
      "ls*": true,
      "cat*": true,
      "git status": true,
      "git diff*": true,
      "git log*": true,
      "npm test": true
    }
  },

  "customInstructions": "Zawsze odpowiadaj po polsku. Używaj przykładów. Commituj małe zmiany.",

  "statusLine": {
    "enabled": true
  },

  "hooks": {
    "preToolCall": "~/.claude/hooks/pre-tool.sh"
  }
}
```

### .claude/settings.json (w projekcie)

```json
{
  "customInstructions": "Projekt React + TypeScript + Tailwind.\n\nGuidelines:\n- Functional components + hooks\n- TypeScript strict mode\n- Tailwind dla stylów\n- React Query dla data fetching\n- Vitest dla testów",

  "autoApproveTools": {
    "Read": ["//**/*.{ts,tsx,json,md}"],
    "Bash": {
      "npm*": true,
      "yarn*": true
    }
  }
}
```

## Zasoby

- **Dokumentacja:** https://code.claude.com/docs
- **GitHub:** https://github.com/anthropics/claude-code
- **MCP Docs:** https://modelcontextprotocol.io/
- **Community:** https://github.com/anthropics/claude-code/discussions

## Quick Reference

```bash
# Setup projektu
mkdir -p .claude/commands
nvim .claude/settings.json

# Slash command
/command arg1 arg2

# Help
/help

# Clear conversation
/clear

# Uprawnienia w settings.json
{
  "autoApproveTools": {
    "Read": ["//path/**"],
    "Bash": {"cmd": true}
  }
}

# Hook (executable!)
chmod +x ~/.claude/hooks/*.sh

# MCP server
npx @modelcontextprotocol/server-name
```

**Zapamiętaj:**
- Bezpieczeństwo > wygoda
- Dokumentuj custom commands
- Testuj hooks przed użyciem
- Nie commituj secrets (.env)
- `.claude/` w repo = team consistency
