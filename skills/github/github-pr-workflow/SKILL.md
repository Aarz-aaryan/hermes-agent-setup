# GitHub PR Workflow — Full Lifecycle

## 1. Create Branch & Make Changes

### get_repository_content
- owner: string (required)
- repo: string (required)
- path: string (required)
- ref: string (optional — branch/commit)

### create_or_update_file_contents
- owner: string (required)
- repo: string (required)
- path: string (required)
- message: string (required)
- content: string (required)
- branch: string (optional)
- sha: string (optional — required when updating existing file)

## 2. Create Pull Request

### create_a_pull_request
- owner: string (required)
- repo: string (required)
- title: string (required)
- body: string (optional)
- head: string (required — source branch)
- base: string (required — target branch, default 'main')
- draft: boolean (default false)
- maintainer_can_modify: boolean (default false)

## 3. Merge

### merge_a_pull_request
- owner: string (required)
- repo: string (required)
- pull_number: number (required)
- commit_title: string (optional)
- commit_message: string (optional)
- merge_method: 'merge' | 'squash' | 'rebase' (default 'merge')
- expected_head_sha: string (optional)

## 4. Auto-Merge

### enable_auto_merge
- owner: string (required)
- repo: string (required)
- pull_number: number (required)
- merge_method: 'squash' | 'merge' | 'rebase' (required)
- author_email: string (optional)
- commit_title: string (optional)
- commit_message: string (optional)

### disable_auto_merge
- owner: string (required)
- repo: string (required)
- pull_number: number (required)

## 5. Update PR

### update_a_pull_request
- owner: string (required)
- repo: string (required)
- pull_number: number (required)
- title: string (optional)
- body: string (optional)
- state: 'open' | 'closed' (optional)
- base: string (optional)
- maintainer_can_modify: boolean (optional)

## 6. Request Reviews

### request_pull_request_reviewers
- owner: string (required)
- repo: string (required)
- pull_number: number (required)
- reviewers: array of usernames (required)
- team_reviewers: array of team slugs (optional)

## 7. Branch Management

### create_a_branch
- owner: string (required)
- repo: string (required)
- branch_name: string (required)
- ref: string (required — source ref)

### list_branches
- owner: string (required)
- repo: string (required)

### delete_a_branch
- owner: string (required)
- repo: string (required)
- branch: string (required)
