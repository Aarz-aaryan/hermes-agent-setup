# Hermes Agent Setup — historical, retired runtime

> **Current status (verified 2026-11-15):** Hermes is no longer the active gateway or scheduler. `aarz-agent.service` runs the Pi replacement; `hermes-gateway.service` is inactive and disabled. This repository is historical configuration, **not a current deployment or complete backup**.
>
> Start with the [current Pi-era system overview](https://github.com/Aarz-aaryan/control-dashboard/blob/main/docs/current-system/README.md), [Discord/scheduler guide](https://github.com/Aarz-aaryan/control-dashboard/blob/main/docs/current-system/agent-server.md), and [Echo/browser voice/WhatsApp guide](https://github.com/Aarz-aaryan/control-dashboard/blob/main/docs/current-system/voice-and-whatsapp.md).
>
> Retained `~/.hermes` paths contain scripts, skills and compatibility assets still used by Pi. Do not delete them blindly. Do not restore or start the old gateway alongside Pi. Historical OpenWA was removed; the separately authorized WhatsApp-Pi service is not the old gateway or scheduled-delivery backend.

The sections below record the **2026-08-25 pre-migration configuration**. Profile/model names and installation instructions are historical, not current operational recommendations.

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

## Historical agy CLI configuration
- **Version:** 1.1.20 (clean install 2026-08-25)
- **Default model:** `flash` (Gemini 3.7 Flash)
- **Invocation:** Historical automation bypassed permission prompts. That is not a recommended default; current headless research needs explicit, narrowly scoped tool permissions.
- **Auth:** OAuth token at `~/.gemini/antigravity-cli/antigravity-oauth-token`

## Historical restore notes — do not execute on the live Pi host

These steps restore the retired Hermes configuration, not the current system. A deliberate rollback requires a separately reviewed recovery plan. They are retained only as historical context.

1. Clone this repo
2. Copy `config.yaml` -> `~/.hermes/config.yaml`
3. Copy profile files -> `~/.hermes/profiles/<profile>/`
4. Copy skills -> `~/.hermes/profiles/aarz/skills/`
5. Add your API keys to `~/.hermes/.env`

## Repository info
- Backup date: 2026-08-25
- Profiles: 6 (aarz, scout, coder, builder, tester, copi)
