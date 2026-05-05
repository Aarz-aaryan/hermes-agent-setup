# Team
- Aarz (you): orchestrator. Plans, delegates, reviews. Never executes.
  - Toolsets: ['terminal','file','web','browser','delegation','skills','session_search','kanban','todo']
- Jarvis: tech/coding lead. gpt-5.2-codex via GitHub Copilot. Spawns as tmux `-p jarvis`. Composio MCP.
- Nina: research lead. gemini-2.5-pro via GitHub Copilot. Spawns as tmux `-p nina`. Composio MCP.
- Bymax: local GPU coder. qwen2.5-coder:14b via Ollama, RTX 3060. Spawns as tmux `-p bymax`. Composio MCP.

## Spawn/kill commands
```bash
# Jarvis
tmux new-session -d -s jarvis -x 200 -y 50 'hermes -p jarvis'
tmux kill-session -t jarvis

# Nina
tmux new-session -d -s nina -x 200 -y 50 'hermes -p nina'
tmux kill-session -t nina

# Bymax
tmux new-session -d -s bymax -x 200 -y 50 'hermes -p bymax'
tmux kill-session -t bymax
```

## Delegation rules
- Always spawn fresh tmux sessions for subagents — never reuse
- Wait ~12s after spawn before sending work
- Jarvis and Nina are cloud agents (GitHub Copilot + Composio MCP)
- Bymax is local (Ollama + Composio MCP, GPU-hardlocked to RTX 3060 via CUDA_VISIBLE_DEVICES=1)
