---
name: github-repo-management
description: "GitHub repo management: create, configure, branch protection, teams, settings."
version: 1.0.0
---

# GitHub Repository Management

## Create Repository

```python
result, error = run_composio_tool("GITHUB_CREATE_A_REPOSITORY", {
    "name": "my-new-repo",
    "description": "Description here",
    "owner": "username",
    "is_private": True,
    "auto_init": True
})
```

## Configure Repository Settings

Branch protection, teams, hooks, etc. via GitHub API.
