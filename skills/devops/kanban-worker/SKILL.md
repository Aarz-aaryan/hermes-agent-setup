# Kanban Worker — Pitfalls and Edge Cases

## Common Issues

### Cards Moving Too Slowly
- Check: is the card actually in 'running'? not just 'ready'?
- If agent is stuck: kill and respawn with revised prompt
- If agent is waiting on external deps: move to blocked with note

### Zombie Cards (stuck in running)
- If an agent dies (tmux session gone), move card back to ready
- Never leave cards in running when agent is gone

### Blockers Not Being Resolved
- Blocked cards need explicit owner and deadline
- A blocked card with no comment = ignored card
- Move to done only when truly done, not "waiting for review"

### Multiple Agents on Same Card
- Don't assign same card to multiple agents
- Split the card if parallel work is needed
- One agent per card in running at a time

## Lane Semantics (enforce strictly)
- **backlog**: unscheduled, raw ideas
- **ready**: spec'd, ready to execute, waiting for agent
- **running**: agent has been assigned and is working
- **review**: code/analysis complete, needs validation
- **blocked**: dependency or external blocker, not agent's fault
- **done**: fully complete with verifiable output

## Lane Transition Rules
- backlog → ready: has spec, clear acceptance criteria
- ready → running: agent assigned
- running → review: agent says complete
- review → done: reviewer validated output
- review → running: quality issues found, send back
- any → blocked: dependency issue identified
- blocked → ready: dependency resolved
