# Claude Code - Configuration and Cheatsheet

Complete guide to configuring and using Claude Code.

## Basic Information

**Claude Code** is the official CLI tool from Anthropic for interacting with Claude in the terminal.

- 🌐 **Official website:** https://code.claude.com/
- 📚 **Documentation:** https://code.claude.com/docs
- 🐙 **GitHub:** https://github.com/anthropics/claude-code

## Installation and Getting Started

### Installation

```bash
# Installation (usually via npm)
npm install -g claude-code

# Or via official installer
curl -fsSL https://code.claude.com/install.sh | sh

# Check version
claude --version
```

### First Launch

```bash
# Launch Claude Code
claude

# Or in a specific directory
cd ~/project
claude

# With a specific file
claude file.py
```

### API Key Configuration

```bash
# Claude Code will automatically ask for API key on first launch
# Or set manually:
export ANTHROPIC_API_KEY="your-api-key-here"

# Add to ~/.bashrc or ~/.zshrc:
echo 'export ANTHROPIC_API_KEY="your-key"' >> ~/.bashrc
```

## Configuration Structure

### File Locations

```
~/.config/claude-code/          # Main configuration folder
├── settings.json               # Global settings
├── .env                        # Environment variables
└── cache/                      # Cache

.claude/                        # Project folder (in repo)
├── commands/                   # Slash commands
│   ├── command1.md
│   └── command2.md
├── settings.json               # Project settings
└── prompts/                    # Custom prompts
```

## settings.json - Configuration

### Location

```bash
# Global configuration
~/.config/claude-code/settings.json

# Project configuration (in repo)
.claude/settings.json
```

### Example Global Configuration

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

  "customInstructions": "Always respond in English. Use specific examples.",

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

### Example Project Configuration

```json
{
  "customInstructions": "This is a React project. Use TypeScript and functional components.",

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

## Permissions (autoApproveTools)

### Allowed Paths for Read/Grep/Glob

```json
{
  "autoApproveTools": {
    "Read": [
      "//home/tomasz/**",           // Entire home directory
      "//**/src/**",                 // All src folders
      "//**/*.{js,ts,py}",          // Specific extensions
      "//home/tomasz/project/**"    // Specific project
    ],
    "Grep": [
      "//home/tomasz/projects/**"
    ],
    "Glob": [
      "//home/tomasz/**"
    ]
  }
}
```

**Pattern syntax:**
- `//` - absolute path
- `*` - any characters (not /)
- `**` - any characters (including /)
- `{js,ts}` - alternatives
- `[0-9]` - character class

### Allowed Bash Commands

```json
{
  "autoApproveTools": {
    "Bash": {
      // Simple commands
      "ls": true,
      "pwd": true,
      "date": true,

      // With arguments (wildcard)
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

**Warning:** Be careful with wildcards! `"rm*": true` would be dangerous.

### Recommended Security Settings

```json
{
  "autoApproveTools": {
    "Read": ["//home/tomasz/**"],
    "Grep": ["//home/tomasz/**"],
    "Glob": ["//home/tomasz/**"],
    "Bash": {
      // Safe read-only commands
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

      // Build tools (usually safe)
      "npm test": true,
      "npm run build": true,
      "cargo build": true,
      "make": true
    }
  }
}
```

**DO NOT add:**
- `rm*` - file deletion
- `sudo*` - commands with sudo
- `dd*` - dangerous disk operations
- `mkfs*` - formatting
- Any destructive commands

## Slash Commands (Custom Commands)

### Creating Slash Commands

```bash
# Create folder for commands
mkdir -p .claude/commands

# Create command
nvim .claude/commands/review.md
```

**Example: `.claude/commands/review.md`**
```markdown
---
description: Code review this file
---

Review this file and find:
1. Potential bugs
2. Performance issues
3. Best practice violations
4. Improvement suggestions

Format as:
- 🐛 Bug: description
- ⚡ Performance: description
- 📖 Best Practice: description
- 💡 Suggestion: description
```

### Usage

```bash
# In Claude Code:
/review path/to/file.js
```

### Example Slash Commands

**`.claude/commands/test.md`**
```markdown
---
description: Write tests for this code
---

Write complete unit tests for {{file}}.
Use the appropriate testing framework for the language.
Cover edge cases and error handling.
```

**`.claude/commands/doc.md`**
```markdown
---
description: Generate documentation
---

Generate complete documentation for {{file}}:
- Function/class descriptions
- Parameters and return values
- Usage examples
- Edge cases

Format: JSDoc / docstrings / rustdoc (depending on language)
```

**`.claude/commands/optimize.md`**
```markdown
---
description: Optimize code
---

Optimize this code for:
1. Performance
2. Readability
3. Memory usage
4. Best practices

Explain each change.
```

**`.claude/commands/translate.md`**
```markdown
---
description: Translate code to another language
---

Translate {{file}} to {{language}}.
Preserve:
- Functionality
- Structure
- Comments
- Error handling

Add comments about differences between languages.
```

### Parameters in Slash Commands

```markdown
<!-- Using variables -->
{{file}}        - current file
{{language}}    - passed parameter
{{selection}}   - selected text
{{arg1}}        - argument 1
{{arg2}}        - argument 2

<!-- Usage example: -->
/translate rust

<!-- In markdown: -->
Translate to {{language}}.
```

## Hooks - Automation

Hooks allow running scripts in response to events.

### Hook Types

1. **userPromptSubmit** - before sending prompt
2. **preToolCall** - before using a tool
3. **postToolCall** - after using a tool

### Configuration in settings.json

```json
{
  "hooks": {
    "userPromptSubmit": "~/.claude/hooks/pre-submit.sh",
    "preToolCall": "~/.claude/hooks/pre-tool.sh",
    "postToolCall": "~/.claude/hooks/post-tool.sh"
  }
}
```

### Example Hook: Pre-Commit Check

**`~/.claude/hooks/pre-tool.sh`**
```bash
#!/bin/bash

# If Claude wants to use git commit, run tests first
if [[ "$TOOL_NAME" == "Bash" ]] && [[ "$TOOL_ARGS" == *"git commit"* ]]; then
    echo "🧪 Running tests before commit..."
    npm test || exit 1
fi

# If everything OK, allow it
exit 0
```

### Example Hook: Auto-format

**`~/.claude/hooks/post-tool.sh`**
```bash
#!/bin/bash

# After editing a file, auto-format
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

### Example Hook: Linting

**`~/.claude/hooks/pre-submit.sh`**
```bash
#!/bin/bash

# Before each prompt, check if repo is clean
if git status --porcelain | grep -q .; then
    echo "⚠️  You have uncommitted changes!"
fi
```

**Remember:**
```bash
# Make hooks executable
chmod +x ~/.claude/hooks/*.sh
```

## MCP Servers (Model Context Protocol)

MCP allows Claude Code to integrate with external tools.

### MCP Configuration

**`~/.config/claude-code/mcp-servers.json`**
```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/home/tomasz/projects"]
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

### Available MCP Servers

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

# Memory (long-term memory)
@modelcontextprotocol/server-memory
```

### Custom MCP Server

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

// Tool definition
server.setRequestHandler('tools/list', async () => {
  return {
    tools: [{
      name: 'get_weather',
      description: 'Get weather for a city',
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
    // Implementation
    return { content: [{ type: 'text', text: 'Sunny, 20°C' }] };
  }
});

const transport = new StdioServerTransport();
server.connect(transport);
```

## Custom Instructions (System Instructions)

### Global Custom Instructions

**`~/.config/claude-code/settings.json`**
```json
{
  "customInstructions": "1. Always respond in English\n2. Use specific examples\n3. For Python code use type hints\n4. Commit small, atomic changes"
}
```

### Per-Project Instructions

**`.claude/settings.json`**
```json
{
  "customInstructions": "This is an e-commerce project in Django.\n\nGuidelines:\n- Use Class-Based Views\n- All API endpoints through DRF\n- Tests in pytest\n- Documentation in docstrings (Google style)\n- Pre-commit hooks: black, flake8, mypy"
}
```

### Advanced Custom Instructions

```json
{
  "customInstructions": "# Role\nYou are an expert in Rust and performance.\n\n# Code Style\n- Use idiomatic Rust\n- Always leverage the type system\n- Error handling through Result<T, E>\n- Documentation with examples\n\n# Testing\n- Unit tests for every function\n- Integration tests for modules\n- Benchmarks for performance-critical code\n\n# Commit Messages\nFormat: <type>(<scope>): <subject>\nTypes: feat, fix, docs, refactor, test, chore"
}
```

## .gitignore for Claude Code

Add to `.gitignore`:

```gitignore
# Claude Code cache
.claude/cache/
.claude/.cache/

# Don't ignore configuration and commands
!.claude/settings.json
!.claude/commands/
!.claude/prompts/

# Ignore logs
.claude/*.log

# API keys (if accidentally in project)
.claude/.env
```

## Useful CLI Commands

```bash
# Run Claude in project
claude

# With specific model
claude --model claude-opus-4

# See version
claude --version

# Help
claude --help

# Reset cache
rm -rf ~/.config/claude-code/cache/

# See current configuration
cat ~/.config/claude-code/settings.json

# Test slash command
# In Claude Code:
/command-name arg1 arg2
```

## Keyboard Shortcuts in Claude Code

| Shortcut | Action |
|-------|-------|
| `Ctrl+C` | Stop generating response |
| `Ctrl+D` | Exit Claude Code |
| `↑/↓` | Prompt history |
| `Tab` | Autocomplete (slash commands) |
| `/help` | List available slash commands |
| `/clear` | Clear conversation |

## Workflow Tips

### 1. Project Setup

```bash
# In new project:
mkdir -p .claude/commands
cat > .claude/settings.json << 'EOF'
{
  "customInstructions": "Project description...",
  "autoApproveTools": {
    "Read": ["//**"],
    "Bash": {
      "npm*": true,
      "git*": true
    }
  }
}
EOF

# Add basic commands
echo "---\ndescription: Code review\n---\nReview code..." > .claude/commands/review.md
```

### 2. Team Configuration

Share `.claude/` in repo:

```bash
git add .claude/
git commit -m "Add Claude Code configuration"
git push
```

Team now has the same:
- Slash commands
- Custom instructions
- Auto-approve rules (if safe)

### 3. Multi-Project Workflow

```bash
# Global configuration for all projects
~/.config/claude-code/settings.json

# + per-project overrides
~/project1/.claude/settings.json
~/project2/.claude/settings.json
```

### 4. Environment Variables

**`.claude/.env`**
```bash
ANTHROPIC_API_KEY=sk-...
GITHUB_TOKEN=ghp_...
DATABASE_URL=postgresql://...
```

**Usage in settings.json:**
```json
{
  "apiKey": "${ANTHROPIC_API_KEY}"
}
```

## Troubleshooting

### Claude doesn't see files

```bash
# Check permissions
ls -la .claude/

# Check settings.json
cat .claude/settings.json

# Add to autoApproveTools
{
  "autoApproveTools": {
    "Read": ["//home/tomasz/**"]
  }
}
```

### Slash command not working

```bash
# Check if file exists
ls .claude/commands/

# Check file format (must be .md)
# Check header:
---
description: Description
---
```

### Hook not executing

```bash
# Check permissions
chmod +x ~/.claude/hooks/*.sh

# Check if path in settings.json is correct
cat ~/.config/claude-code/settings.json | grep hooks

# Debug hook
bash -x ~/.claude/hooks/pre-tool.sh
```

### MCP server not working

```bash
# Check if server is installed
npx @modelcontextprotocol/server-filesystem --version

# Check logs
~/.config/claude-code/logs/mcp-*.log

# Test manually
npx @modelcontextprotocol/server-filesystem /path/to/dir
```

## Best Practices

### 1. Security

```json
{
  "autoApproveTools": {
    // ✅ Good - read-only
    "Read": ["//home/tomasz/projects/**"],
    "Grep": ["//home/tomasz/projects/**"],

    // ❌ Bad - too broad permissions
    "Bash": { "*": true },

    // ✅ Good - specific commands
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
├── settings.json              # Project configuration
├── commands/                  # Slash commands
│   ├── review.md
│   ├── test.md
│   └── doc.md
├── prompts/                   # Reusable prompts
│   └── code-style.md
└── .env                       # Secrets (in .gitignore!)
```

### 3. Documentation

Document custom commands:

**`README.md`**
```markdown
## Claude Code Commands

- `/review` - Code review of file
- `/test` - Generate tests
- `/doc` - Generate documentation
- `/optimize` - Optimize code
```

### 4. Team Sharing

```bash
# Commit only safe things
git add .claude/settings.json
git add .claude/commands/

# DO NOT commit
.claude/.env          # Secrets
.claude/cache/        # Cache
```

## Example Complete Setup

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

  "customInstructions": "Always respond in English. Use examples. Commit small changes.",

  "statusLine": {
    "enabled": true
  },

  "hooks": {
    "preToolCall": "~/.claude/hooks/pre-tool.sh"
  }
}
```

### .claude/settings.json (in project)

```json
{
  "customInstructions": "React + TypeScript + Tailwind project.\n\nGuidelines:\n- Functional components + hooks\n- TypeScript strict mode\n- Tailwind for styles\n- React Query for data fetching\n- Vitest for tests",

  "autoApproveTools": {
    "Read": ["//**/*.{ts,tsx,json,md}"],
    "Bash": {
      "npm*": true,
      "yarn*": true
    }
  }
}
```

## Resources

- **Documentation:** https://code.claude.com/docs
- **GitHub:** https://github.com/anthropics/claude-code
- **MCP Docs:** https://modelcontextprotocol.io/
- **Community:** https://github.com/anthropics/claude-code/discussions

## Quick Reference

```bash
# Project setup
mkdir -p .claude/commands
nvim .claude/settings.json

# Slash command
/command arg1 arg2

# Help
/help

# Clear conversation
/clear

# Permissions in settings.json
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

**Remember:**
- Security > convenience
- Document custom commands
- Test hooks before using
- Don't commit secrets (.env)
- `.claude/` in repo = team consistency
