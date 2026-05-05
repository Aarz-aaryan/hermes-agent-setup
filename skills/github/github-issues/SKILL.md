# GitHub Issues — Create, Triage, Label, Assign

## create_an_issue
- owner: string (required)
- repo: string (required)
- title: string (required)
- body: string (optional)
- labels: array of label names (optional, not ids)
- assignees: array of usernames (optional)
- milestone: number (optional — milestone number)
- state: 'open' | 'closed' (default 'open')

## list_repo_issues
- owner: string (required)
- repo: string (required)
- milestone: number | '*' | 'none' (optional)
- state: 'open' | 'closed' | 'all' (default 'open')
- labels: comma-separated label names (optional)
- sort: 'created' | 'updated' | 'comments' (default 'created')
- direction: 'asc' | 'desc' (default 'desc')
- since: ISO date string (optional)
- per_page: number (default 30, max 100)
- page: number (default 1)

## get_an_issue
- owner: string (required)
- repo: string (required)
- issue_number: number (required)

## update_an_issue
- owner: string (required)
- repo: string (required)
- issue_number: number (required)
- title: string (optional)
- body: string (optional)
- state: 'open' | 'closed' (optional)
- labels: array of label names (optional)
- assignees: array of usernames (optional)
- milestone: number | null (optional)

## add_issue_comment
- owner: string (required)
- repo: string (required)
- issue_number: number (required)
- body: string (required)

## list_issue_comments
- owner: string (required)
- repo: string (required)
- issue_number: number (required)
- per_page: number (default 30, max 100)
- page: number (default 1)

## lock_issue
- owner: string (required)
- repo: string (required)
- issue_number: number (required)
- lock_reason: 'off-topic' | 'too heated' | 'resolved' | 'spam' (optional)

## unlock_issue
- owner: string (required)
- repo: string (required)
- issue_number: number (required)

## list_repo_labels
- owner: string (required)
- repo: string (required)
- per_page: number (default 30, max 100)
- page: number (default 1)

## create_a_label
- owner: string (required)
- repo: string (required)
- name: string (required)
- color: string (required — 6 char hex without #)
- description: string (optional)

## update_a_label
- owner: string (required)
- repo: string (required)
- name: string (required)
- new_name: string (optional)
- color: string (optional)
- description: string (optional)

## delete_a_label
- owner: string (required)
- repo: string (required)
- name: string (required)

## add_labels_to_issue
- owner: string (required)
- repo: string (required)
- issue_number: number (required)
- labels: array of label names (required)

## remove_label_from_issue
- owner: string (required)
- repo: string (required)
- issue_number: number (required)
- name: string (required)

## list_milestones
- owner: string (required)
- repo: string (required)
- state: 'open' | 'closed' | 'all' (default 'open')
- sort: 'due_on' | 'completeness' | 'created' | 'updated' | 'GHMS' (default 'due_on')
- direction: 'asc' | 'desc' (default 'asc')
- per_page: number (default 30, max 100)
- page: number (default 1)

## create_a_milestone
- owner: string (required)
- repo: string (required)
- title: string (required)
- state: 'open' | 'closed' (default 'open')
- description: string (optional)
- due_on: ISO date string (optional)

## update_a_milestone
- owner: string (required)
- repo: string (required)
- milestone_number: number (required)
- title: string (optional)
- state: 'open' | 'closed' (optional)
- description: string (optional)
- due_on: ISO date string (optional)

## delete_a_milestone
- owner: string (required)
- repo: string (required)
- milestone_number: number (required)

## add_assignees_to_issue
- owner: string (required)
- repo: string (required)
- issue_number: number (required)
- assignees: array of usernames (required)

## remove_assignees_from_issue
- owner: string (required)
- repo: string (required)
- issue_number: number (required)
- assignees: array of usernames (required)

## check_user_repo_collaborator_status
- owner: string (required)
- repo: string (required)
- username: string (required)

## list_issue_events
- owner: string (required)
- repo: string (required)
- issue_number: number (required)
- per_page: number (default 30, max 100)
- page: number (default 1)

## timeline_issues_events
- owner: string (required)
- repo: string (required)
- issue_number: number (required)
- per_page: number (default 30, max 100)
- page: number (default 1)
