---
name: agent-delegation-protocol
description: "Protocol for delegating tasks between sub-agents."
version: 1.0.0
---

# Agent Delegation Protocol

Protocol for effective task delegation between sub-agents in the Hermes multi-agent system.

## When to Delegate

- Task requires different expertise
- Parallel execution would be faster
- Isolation needed for safety

## Delegation Patterns

1. **Extract & Delegate** - Pull out the subtask, delegate, merge results
2. **Supervisor Pattern** - Main agent coordinates sub-agents
3. **Hierarchical** - Multiple levels of delegation
