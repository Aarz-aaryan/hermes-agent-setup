---
name: webhook-subscriptions
description: "Webhook subscriptions for event-driven agent runs."
version: 1.1.0
---

# Webhook Subscriptions

Create dynamic webhook subscriptions for external services.

## Setup

```bash
hermes webhook subscribe <name> \
  --prompt "Prompt template" \
  --events "event1,event2" \
  --deliver telegram \
  --deliver-chat-id "12345"
```

## Supported Events

GitHub, GitLab, Stripe, CI/CD, and more.
