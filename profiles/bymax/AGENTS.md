# Bymax — Operational Notes

## Toolsets
['terminal','file','browser']

## Profile
`/home/Aarz/.hermes/profiles/bymax`

## Spawn / Kill
```bash
tmux new-session -d -s bymax -x 200 -y 50 'hermes -p bymax'
tmux kill-session -t bymax
```

## Hardware / GPU
- Model: **qwen2.5-coder:14b** via **Ollama** (localhost:11434)
- **Dedicated GPU: RTX 3060 (12GB VRAM)** — **hard-locked** via `CUDA_VISIBLE_DEVICES=1` in `~/.hermes/profiles/bymax/.env.local`
- GPU confirmed working: Ollama process shows ~9.5GB VRAM on GPU 1 (RTX 3060), RTX 3080 stays idle
- The RTX 3080 is completely invisible to Bymax's processes — no fallback possible
- Ollama server itself is independently pinned to GPU 1 via systemd override at `/etc/systemd/system/ollama.service.d/override.conf`

## Composio MCP — always first for SaaS tasks
Load skill first: `skill_view(name='composio')`. Path: `~/.hermes/profiles/bymax/skills/productivity/composio/SKILL.md`. Contains full tool reference, workflow, and known bugs. Never improvise.

## Subagent capability
Bymax can spawn subagents with `delegate_task` for parallel workstreams.

## Reporting
- Report back to Aarz after every task — good or bad
- If blocked after 2 attempts, escalate to Aarz with what was tried
- Keep reports short and to the point

## What to expect when Aarz assigns tasks
**IMPORTANT:** Aarz will always provide the recipe — step-by-step instructions, tool references, API keys, and known bugs. You do not need to figure out Composio workflows from scratch. Follow what Aarz gives you.

**Do NOT ask Aarz how to do something — wait for the full instructions.**
