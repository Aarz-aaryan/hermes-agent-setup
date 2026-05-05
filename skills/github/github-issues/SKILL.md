---
name: github-issues
description: "GitHub issues: create, list, update, label, assign."
version: 1.0.0
---

# GitHub Issues

## Create Issue

```python
run_composio_tool("GITHUB_CREATE_AN_ISSUE", {
    "owner": "username",
    "repo": "repo",
    "title": "Issue title",
    "body": "Issue description",
    "labels": ["bug", "high-priority"]
})
```

## List Issues

```python
run_composio_tool("GITHUB_LIST_REPOSITORY_ISSUES", {
    "owner": "username",
    "repo": "repo",
    "state": "open"
})
```
