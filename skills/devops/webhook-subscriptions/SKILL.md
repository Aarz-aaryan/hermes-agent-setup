# Webhook Subscriptions — Event-Driven Agent Runs

## Concept
Webhooks allow external events (GitHub PR, Stripe payment, etc.) to trigger Hermes agent runs automatically.

## Setup

### 1. Create a webhook subscription
```
hermes webhooks create --url https://your-agent.com/webhook --events github.pull_request.opened,github.issue.comment --name my-webhook
```

### 2. Configure the agent prompt
In the webhook config, set a trigger prompt:
```yaml
webhooks:
  my-webhook:
    trigger_prompt: |
      A new GitHub PR was just opened by {{event.payload.pull_request.user.login}}:
      - Repo: {{event.payload.repository.full_name}}
      - PR #: {{event.payload.pull_request.number}}
      - Title: {{event.payload.pull_request.title}}
      - URL: {{event.payload.pull_request.html_url}}
```

### 3. Verify the webhook
```
hermes webhooks verify --name my-webhook
```

## Available Events

### GitHub
- `github.push` — any push
- `github.pull_request.opened` — PR opened
- `github.pull_request.closed` — PR closed/merged
- `github.issue.opened` — issue opened
- `github.issue.comment` — issue comment
- `github.check_run.completed` — CI check completed
- `github.release.published` — release published

### Generic
- `http.post` — any POST to the webhook URL
- `schedule.cron` — cron-triggered

## Payload Access
Use `{{event.payload.path.to.field}}` in trigger prompts.

## Debugging
```
hermes webhooks list
hermes webhooks logs --name my-webhook
hermes webhooks test --name my-webhook --payload '{"test": true}'
```
