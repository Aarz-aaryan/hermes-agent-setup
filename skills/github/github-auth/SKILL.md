---
name: github-auth
description: "GitHub authentication setup for Hermes Agent."
version: 1.0.0
---

# GitHub Auth

Setup GitHub authentication for Hermes Agent via Composio.

## Configuration

Add to your profile config:
```yaml
mcp_servers:
  github:
    command: npx
    args: ["-y", "@modelcontextprotocol/server-github"]
    env:
      GITHUB_PERSONAL_ACCESS_TOKEN: YOUR_GITHUB_TOKEN
```

## Permissions Required

- repo (full control)
- issues
- pull_requests
