# Kanban Orchestrator — Project Management Playbook

## Board Structure
- **backlog**: unscheduled tasks
- **ready**: planned, ready to pick up
- **running**: actively being worked
- **review**: waiting for review/validation
- **blocked**: cannot proceed
- **done**: completed

## Workflow
1. **Intake** — decompose project into tasks, add to backlog
2. **Plan** — move tasks from backlog → ready (prioritized)
3. **Execute** — assign and move ready → running
4. **Review** — validate output, move running → review → done (or blocked)
5. **Blocker resolution** — blocked → ready when resolved

## Specialist Roster Conventions
- **Nina** (research): owns research tasks, data analysis, literature reviews
- **Jarvis** (coding): owns implementation tasks, PRs, code reviews
- **Bymax** (local coding): owns GPU-heavy tasks, local model inference

## Task Decomposition Principles
- Each card should be: specific, actionable, verifiable
- Break epics into cards completable in < 1 day
- Each card should have clear acceptance criteria
- Dependencies should be explicit

## Card Fields
- Title: verb + object
- Description: context, links, acceptance criteria
- Assignee: the responsible agent
- Priority: P0/P1/P2/P3
- Blocked by: card IDs this depends on
- Labels: category tags

## Hermes Kanban Commands
- `kanban init <board>` — create board
- `kanban create <title> --board <board>` — add card
- `kanban list --board <board>` — show board
- `kanban show <id>` — card details
- `kanban move <id> <lane>` — move card
- Board URL: http://100.100.35.6:3000
