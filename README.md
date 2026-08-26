# Hermes Agent Setup

Complete backup of the Hermes Agent multi-agent system.

## What's included
- `config.yaml` — root Hermes config
- `profiles/` — 6 agent profiles:
  - `aarz` — orchestrator (MiniMax-M2.7)
  - `scout` — research specialist (MiniMax-M2.7 + agy/Gemini 3.7 Flash)
  - `coder` — code specialist (MiniMax-M2.7 + agy/Gemini 3.7 Pro)
  - `builder` — DevOps/automation specialist (MiniMax-M2.7)
  - `tester` — QA/E2E specialist (MiniMax-M2.7)
  - `copi` — Copilot CLI secondary (gpt-5.3-codex)
- `skills/` — skill files (SKILL.md)
- `plugins/` — scout-routing, mnemosyne, hermes-achievements

## What's NOT included (by design)
Sessions, memories, logs, state databases, auth files, caches, and API keys are excluded. Restore these separately.

## Profile summary

| Profile | Model | Role |
|---------|-------|------|
| aarz | MiniMax-M2.7 | Orchestrator — plans, delegates, synthesizes |
| scout | MiniMax-M2.7 + agy/flash | Research — cited multi-angle web research |
| coder | MiniMax-M2.7 + agy/pro | Code — generation, refactor, debug, PR review |
| builder | MiniMax-M2.7 | DevOps — scripts, ssh, cron, deploy |
| tester | MiniMax-M2.7 | QA — tests, browser automation, audits |
| copi | gpt-5.3-codex | Overflow — GitHub Copilot CLI (agy at capacity) |

## agy CLI (primary workhorse)
- **Version:** 1.1.20 (clean install 2026-08-25)
- **Default model:** `flash` (Gemini 3.7 Flash)
- **Invocation:** `~/.local/bin/agy -p "TASK" --dangerously-skip-permissions [--model pro]`
- **Auth:** OAuth token at `~/.gemini/antigravity-cli/antigravity-oauth-token`

## To restore
1. Clone this repo
2. Copy `config.yaml` -> `~/.hermes/config.yaml`
3. Copy profile files -> `~/.hermes/profiles/<profile>/`
4. Copy skills -> `~/.hermes/profiles/aarz/skills/`
5. Add your API keys to `~/.hermes/.env`

## Repository info
- Backup date: 2026-08-25
- Profiles: 6 (aarz, scout, coder, builder, tester, copi)
