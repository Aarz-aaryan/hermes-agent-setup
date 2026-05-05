# Codex — OpenAI Codex CLI for Coding

## Overview
OpenAI Codex CLI is a local coding agent that runs in your terminal. It's the fastest way to get a capable coding agent going.

## Installation
```bash
npm install -g @openai/codex
# or
brew install codex
```

## Authentication
```bash
codex auth
# Opens browser for OAuth with OpenAI
```

## Usage

### Interactive Mode
```bash
codex
# Opens interactive REPL
```

### Single Task Mode
```bash
codex --prompt "Fix the bug in main.py"
codex --cli "create a new FastAPI endpoint"
```

### Project Mode (recommended)
```bash
mkdir my-project
cd my-project
codex --init  # Creates .codex.json config
codex        # Runs in project context
```

## .codex.json Config
```json
{
  "model": "gpt-4o",
  "api_key": "...",
  "auto_test": false,
  "test_cmd": "pytest",
  "languages": ["python", "javascript"],
  "exclude": ["node_modules", "dist", "*.pyc"]
}
```

## Features

### Inline Edits
Codex can edit files in place without rewriting whole files.

### Multiple Files
Can work across multiple files simultaneously.

### Bash Commands
Can run shell commands: `npm test`, `git commit`, etc.

### Git Integration
Automatic commit messages and optional auto-commit.
```bash
codex --git "commit all changes with a good message"
```

### Code Search
```bash
codex --search "find all uses of this function"
```

## MCP Server Mode
Run Codex as an MCP server for other tools to use:
```bash
codex --mcp
# Runs on stdio, can be connected to Hermes MCP
```

## Tips
- Give Codex a specific goal, not vague instructions
- Use project mode for multi-file work
- Set `auto_test: true` for TDD workflow
- Exclude large directories in `.codex.json`

## Known Issues
- Codex can be verbose — specify "be concise" in prompt
- May occasionally misread file state — use `git diff` to verify
- API costs money — set spending limits in OpenAI dashboard

## Workspace Path
User's Codex config: `~/.codex/`
Project config: `./.codex.json`
