# Agent Delegation Protocol

## Core Principle
Delegation is not distribution — it is placing full responsibility on a capable agent. The parent never re-executes what it delegates. Trust the agent's output or kill and respawn.

## When to Delegate
- Task is a self-contained subtask
- Another agent has the right comparative advantage
- Reasoning-heavy work that would bloat the parent's context
- Parallel independent workstreams

## When NOT to Delegate
- Mechanical multi-step work → use execute_code or terminal
- Single tool call → just call the tool directly
- Task requiring user interaction → subagent cannot use clarify
- Durable long-running work → use cronjob or background terminal

## How to Spawn
```
tmux new-session -d -s <name> -x 200 -y 50 'hermes -p <profile>'
```
Wait ~12s for startup. Send mission: `tmux send-keys -t <name> '<mission>' Enter`. Monitor: `tmux capture-pane -t <name> -p | tail -N`.

### Agent Roster
- **Jarvis** (`-p jarvis`): coding lead. gpt-5.2-codex. Composio MCP.
- **Nina** (`-p nina`): research lead. gemini-2.5-pro. Composio MCP.
- **Bymax** (`-p bymax`): local coding. qwen2.5-coder:14b via Ollama. RTX 3060.

## What to Delegate
Each subagent gets:
1. A clear, self-contained goal
2. All necessary context (file paths, error messages, project structure, constraints)
3. Constraints
4. Nothing else

Subagents have NO memory of parent conversation.

## Monitoring
- Light: `tmux capture-pane -t <name> -p`
- Kill: `tmux kill-session -t <name>`
- Respawn: same tmux new-session command

## Output Validation
- Review all agent output
- Verify external side-effects
- If quality is substandard, send a correction mission

## Composio Note
Agents use Composio for external SaaS. All params are FLAT (no "parameters" wrapper). Use `session_id` from `COMPOSIO_SEARCH_TOOLS`.

## delegation.max_spawn_depth
- Default is 1: subagents cannot spawn their own subagents
- If nested delegation is needed, set `max_spawn_depth: 2` and use `role: orchestrator`
