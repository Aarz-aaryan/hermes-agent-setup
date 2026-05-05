# Autonomous AI Agents — Skills for Running Independent Coding Agents

## Overview
Run autonomous AI coding agents as separate processes. These agents work independently, can spawn subagents, and coordinate parallel workstreams.

## Available Agents

### Claude Code
See `claude-code` skill.

### OpenAI Codex CLI
See `codex` skill.

### OpenCode CLI
See `opencode` skill.

## Architecture Patterns

### 1. Single Agent (simplest)
Spawn one agent to handle one task.
```bash
tmux new-session -d -s agent1 'claude --acp --stdio'
```

### 2. Parallel Agents (independent tasks)
Spawn multiple agents simultaneously for independent workstreams.
```bash
tmux new-session -d -s agent1 'claude --acp --stdio'
tmux new-session -d -s agent2 'claude --acp --stdio'
tmux new-session -d -s agent3 'claude --acp --stdio'
```

### 3. Orchestrator + Workers (hierarchical)
Orchestrator spawns workers, assigns tasks, aggregates results.
```
Orchestrator
├── Worker A (task 1)
├── Worker B (task 2)
└── Worker C (task 3)
```

### 4. Sequential Handoffs (pipeline)
Agent A completes, hands off to B, who hands off to C.
```
Agent A → Agent B → Agent C → Final Output
```

## Agent Lifecycle Management

### Start
```bash
tmux new-session -d -s <name> 'agent-command'
```

### Send Mission
```bash
tmux send-keys -t <name> '<mission description>' Enter
```

### Monitor
```bash
tmux capture-pane -t <name> -p | tail -50
```

### Interrupt
```bash
tmux send-keys -t <name> C-c  # Ctrl+C
```

### Kill
```bash
tmux kill-session -t <name>
```

### Respawn (after kill)
```bash
tmux new-session -d -s <name> 'agent-command'
```

## Mission Design

### Good Mission
```
Implement a REST API for a todo app using FastAPI.
- POST /todos — create todo
- GET /todos — list all todos
- PUT /todos/{id} — update todo
- DELETE /todos/{id} — delete todo
- Use SQLite for storage
- Write tests for all endpoints
- Store in /tmp/todo-api/
```

### Bad Mission (too vague)
```
Make a todo app
```

## Coordination

### Shared State
Use files or a database for agents to share state.
```bash
# Agent A writes
echo "status=complete" > /tmp/shared/status.txt

# Agent B reads
source /tmp/shared/status.txt
```

### Results Aggregation
Collect outputs from all agents after parallel completion.
```bash
for name in agent1 agent2 agent3; do
  tmux capture-pane -t $name -p | tail -20 >> /tmp/results.txt
done
```

## Spawning from Hermes
```
delegate_task(
  goal: "<mission>",
  role: "leaf",  # or "orchestrator"
  toolsets: ["terminal", "file", "web"],
  context: "<background context>"
)
```
