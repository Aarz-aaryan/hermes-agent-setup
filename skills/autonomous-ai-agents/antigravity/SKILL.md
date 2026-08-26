---
name: antigravity
description: "agy CLI dispatch — Google's terminal coding agent. agy 1.1.20, --dangerously-skip-permissions, Pro/Flash models."
version: 3.0.0
author: Aarz
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [Coding-Agent, Antigravity, Google, Gemini-3, terminal-oneshot, delegation-target, dispatch]
    related_skills: [github-copilot, codex, claude-code, opencode, hermes-agent]
---

# agy CLI — Quick Reference (v3.0.0, clean install 2026-08-25)

**agy 1.1.20** installed via official `curl -fsSL https://antigravity.google/cli/install.sh | bash`.
OAuth token carried over from previous install. No wrapper script needed.

## Canonical invocation

```bash
agy -p "TASK" --dangerously-skip-permissions [--model MODEL] [--print-timeout DURATION]
```

- `--dangerously-skip-permissions` — **always required** for unattended/headless use
- `--model` — optional, defaults to `flash` (Gemini 3.7 Flash)
- `--print-timeout` — optional, default `5m0s`

## Available models

| Alias | Display name | Use case |
|---|---|---|
| `flash` | Gemini 3.7 Flash | Default, fast research, simple code |
| `flash_lite` | Gemini Flash Lite | Ultra-fast lookups, trivial tasks |
| `pro` | Gemini 3.7 Pro | Deep refactors, complex logic, multi-step |
| `inherit` | Inherit Parent Model | Use parent conversation's model |

**Default is `flash`** (Gemini 3.7 Flash). Use `--model pro` for complex tasks.

## Common patterns

```bash
# Fast task (default flash)
/home/Aarz/.local/bin/agy -p "Fix the bug in auth.py" --dangerously-skip-permissions

# Complex task (Pro)
/home/Aarz/.local/bin/agy -p "Refactor the entire auth module" --model pro --dangerously-skip-permissions

# With custom timeout
/home/Aarz/.local/bin/agy -p "Research X" --dangerously-skip-permissions --print-timeout 3m

# Structured output (JSON)
/home/Aarz/.local/bin/agy -p "List files" --dangerously-skip-permissions --output-format json
```

## OAuth / Auth
- Token lives at `~/.gemini/antigravity-cli/antigravity-oauth-token`
- If auth fails: run `agy` interactively in a terminal with a browser, authenticate once
- Token persists across updates — no need to re-auth on new installs

## What changed from v2 (old wrapper era)
- **No wrapper script** — the old `agy-cli.sh` wrapper + `chattr +i` locked binary is gone
- **OAuth fixed** — 1.0.9/1.0.10 regression is resolved in 1.1.20
- **No `update` trap** — the substring blocking bug is gone
- **No GODEBUG needed** — 1.1.x handles IPv6/HTTP2 correctly
- **Default model changed** — now `flash` (3.7 Flash), was `pro` (3.1 Pro)

## Quick test
```bash
agy -p "Say hello" --dangerously-skip-permissions
```
