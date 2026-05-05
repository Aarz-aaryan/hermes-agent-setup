# Agent Health Check — Monitor All Agent Profiles

## Concept
Check the health status of all agent profiles (bymax, jarvis, nina, aarz) to see if they are running, responding, and have valid credentials.

## Checks Per Agent

### 1. Process Check
Is there a tmux session running for this agent?
```bash
tmux has-session -t <agent-name> 2>/dev/null && echo "running" || echo "not running"
```

### 2. Model Availability
Can the agent's model respond?
```bash
curl -s http://localhost:PORT/health  # if they expose a health endpoint
# or
timeout 10 hermes -p <agent> --health-check 2>&1 | head -5
```

### 3. Credential Check
Does the agent have valid API keys?
```bash
grep -r "API_KEY\|TOKEN\|SECRET" ~/.hermes/profiles/<agent>/.env 2>/dev/null
```

### 4. Recent Activity
Is the agent actively working or idle?
```bash
tmux capture-pane -t <agent> -p | tail -5
```

## Automated Health Check Script

```bash
#!/bin/bash
AGENTS="bymax jarvis nina aarz"

for agent in $AGENTS; do
    echo "=== $agent ==="
    
    # Process check
    if tmux has-session -t $agent 2>/dev/null; then
        echo "  Process: RUNNING"
        
        # Activity check
        last_activity=$(tmux capture-pane -t $agent -p | tail -1)
        echo "  Last output: $last_activity"
    else
        echo "  Process: NOT RUNNING"
    fi
    
    # Config check
    if [ -f ~/.hermes/profiles/$agent/config.yaml ]; then
        echo "  Config: EXISTS"
    else
        echo "  Config: MISSING"
    fi
    
    echo ""
done
```

## Health Check Output Format
```
=== bymax ===
  Process: RUNNING
  Model: qwen2.5-coder:14b
  GPU: RTX 3060 — 3.2GB/6GB used
  Status: IDLE (since 14:32)

=== jarvis ===
  Process: RUNNING
  Model: gpt-5.2-codex
  Status: WORKING (current task: refactoring auth)

=== nina ===
  Process: RUNNING
  Model: gemini-2.5-pro
  Status: WORKING (current task: research report)

=== aarz ===
  Process: (orchestrator — runs in current session)
  Model: MiniMax-M2.7
  Status: ACTIVE
```

## When to Restart
- Process not running → restart immediately
- Model not responding (timeout after 30s) → restart
- GPU memory exhausted → restart bymax
- Credential error → check .env files, restart

## Restart Command
```bash
tmux kill-session -t <agent>
tmux new-session -d -s <agent> 'hermes -p <agent>'
sleep 12
tmux send-keys -t <agent> 'echo "Ready"' Enter
```
