---
name: github-pr-workflow
description: "GitHub PR workflow: create, review, merge, automate."
version: 1.0.0
---

# GitHub PR Workflow

## Create PR

```python
run_composio_tool("GITHUB_CREATE_A_PULL_REQUEST", {
    "owner": "username",
    "repo": "repo-name",
    "title": "PR title",
    "body": "PR description",
    "head": "feature-branch",
    "base": "main"
})
```

## Review and Merge

Automated PR review and merge workflows.
