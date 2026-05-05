# Hermes Agent Setup

Complete backup of my Hermes Agent multi-agent system. This repo contains:

- `config.yaml` — root Hermes config
- `profiles/` — 4 agent profiles (aarz, bymax, jarvis, nina): config.yaml, SOUL.md, AGENTS.md
- `skills/` — 92 skill files (SKILL.md) across all categories

## What's NOT included (by design)

Sessions, memories, logs, state databases, auth files, caches, and API keys are excluded. Restore these separately.

## To restore

1. Clone this repo
2. Copy `config.yaml` → `~/.hermes/config.yaml`
3. Copy profile files → `~/.hermes/profiles/<name>/`
4. Copy skills → `~/.hermes/skills/`
5. Add your API keys to `~/.hermes/.env`

## Repository info

- Repo: [Aarz-aaryan/hermes-agent-setup](https://github.com/Aarz-aaryan/hermes-agent-setup)
- Backed up: 2026-05-05
- Files: 107 (config + profiles + skills)
