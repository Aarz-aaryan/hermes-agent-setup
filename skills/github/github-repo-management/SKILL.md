# GitHub Repository Management

## create_a_github_repository
- name: string (required)
- owner: string (required — username or org)
- description: string (optional)
- private: boolean (default false)
- auto_init: boolean (default false)
- has_issues: boolean (default true)
- has_projects: boolean (default false)
- has_wiki: boolean (default false)
- has_discussions: boolean (default false)
- has_downloads: boolean (default false)
- license_template: string (optional)
- gitignore_template: string (optional)

## delete_a_github_repository
- owner: string (required)
- repo: string (required)

## get_a_github_repository
- owner: string (required)
- repo: string (required)

## list_github_repositories
- per_page: number (default 30, max 100)
- sort: 'created' | 'updated' | 'pushed' | 'full_name' (default 'full_name')
- direction: 'asc' | 'desc'
- affiliation: comma-separated: 'owner', 'collaborator', 'organization_member'
- type: 'all' | 'owner' | 'member'

## update_github_repository
- owner: string (required)
- repo: string (required)
- name: string (optional)
- description: string (optional)
- private: boolean (optional)
- has_issues: boolean (optional)
- has_projects: boolean (optional)
- has_wiki: boolean (optional)
- default_branch: string (optional)
- allow_auto_merge: boolean (optional)
- allow_forking: boolean (optional)
- delete_branch_on_merge: boolean (optional)
- archived: boolean (optional)
- visibility: 'public' | 'private' | 'internal'
- is_template: boolean (optional)

## fork_a_github_repository
- owner: string (required)
- repo: string (required)
- organization: string (optional — org to fork into)

## list_repository_teams
- per_page: number (default 30, max 100)
- page: number (default 1)

## transfer_github_repository
- owner: string (required)
- repo: string (required)
- new_owner: string (required)
- new_name: string (optional)
- team_slugs: array of team slugs (optional)

## enable_vulnerability_alert
- owner: string (required)
- repo: string (required)

## disable_vulnerability_alert
- owner: string (required)
- repo: string (required)

## list_public_github_repositories
- since: Unix timestamp (optional)
- per_page: number (default 30, max 100)

## search_github_repositories
- query: string (required, see GitHub search syntax)
- sort: 'stars' | 'forks' | 'help-wanted-issues' | 'updated'
- order: 'asc' | 'desc' (default 'desc')
- per_page: number (default 30, max 100)
- page: number (default 1)

### search syntax examples
- `qwen in:name` — repo name contains qwen
- `qwen in:readme` — readme contains qwen
- `qwen in:description` — description contains qwen
- `stars:>1000` — more than 1000 stars
- `forks:>100` — more than 100 forks
- `pushed:>2024-01-01` — pushed after date
- `language:python` — Python repos
- `user:octocat` — repos owned by octocat
- `org:microsoft` — repos owned by microsoft org

## get_repository_content
- owner: string (required)
- repo: string (required)
- path: string (required)
- ref: string (optional — branch/commit/tag)

Returns: { content: Base64 encoded string (if file), type: 'file' | 'dir' | 'symlink' | 'submodule', content[]: (if dir) }

## create_or_update_file_contents
- owner: string (required)
- repo: string (required)
- branch: string (optional)
- path: string (required)
- message: string (required)
- content: string (required — Base64 encoded or plain string)
- sha: string (optional — required for updates)
- committer: { name, email, date } (optional)
- author: { name, email, date } (optional)

## commit_multiple_files
- owner: string (required)
- repo: string (required)
- branch: string (required)
- message: string (required)
- upserts: array of { path, content, encoding } (required — at least one)
- deletes: array of string paths (optional)
- author: { name, email, date } (optional)
- committer: { name, email, date } (optional)
- base_branch: string (optional — for new branches)

## delete_file
- owner: string (required)
- repo: string (required)
- branch: string (optional)
- path: string (required)
- message: string (required — commit message)
- sha: string (required)
- committer: { name, email, date } (optional)
- author: { name, email, date } (optional)

## get_a_tree
- owner: string (required)
- repo: string (required)
- tree_sha: string (required — branch name, commit SHA, or 'HEAD~N')
- recursive: boolean (default false)

## list_branches
- owner: string (required)
- repo: string (required)
- per_page: number (default 30, max 100)
- page: number (default 1)

## get_a_branch
- owner: string (required)
- repo: string (required)
- branch: string (required)

## create_a_branch
- owner: string (required)
- repo: string (required)
- branch_name: string (required)
- ref: string (required — source ref to branch from)

## delete_a_branch
- owner: string (required)
- repo: string (required)
- branch: string (required)

## merge_branches
- owner: string (required)
- repo: string (required)
- base: string (required)
- head: string (required — can be comma-separated for multiple heads)
- commit_message: string (optional)

## compare_two_commits
- owner: string (required)
- repo: string (required)
- basehead: string (required — 'BASE...HEAD' format)
- page: number (default 1)
- per_page: number (default 30, max 100)

## get_a_reference
- owner: string (required)
- repo: string (required)
- ref: string (required — 'heads/branch', 'tags/tag', 'pull/N/head')

## list_matching_references
- owner: string (required)
- repo: string (required)
- query: string (required — e.g. 'heads/' or 'tags/')

## create_or_update_a_release
- owner: string (required)
- repo: string (required)
- tag_name: string (required)
- target_commitish: string (optional)
- name: string (optional)
- body: string (optional)
- draft: boolean (default false)
- prerelease: boolean (default false)
- generate_release_notes: boolean (default false)

## list_releases
- owner: string (required)
- repo: string (required)
- per_page: number (default 30, max 100)
- page: number (default 1)

## get_release
- owner: string (required)
- repo: string (required)
- release_id: number (required)

## delete_a_release
- owner: string (required)
- repo: string (required)
- release_id: number (required)

## get_latest_release
- owner: string (required)
- repo: string (required)

## get_a_repo_language_breakdown
- owner: string (required)
- repo: string (required)

## get_repo_statistics
- owner: string (required)
- repo: string (required)
- timerange: 'last_year' | 'all_time' (default 'last_year')

## list_repo_tags
- owner: string (required)
- repo: string (required)
- per_page: number (default 30, max 100)
- page: number (default 1)

## enable_automated_security_fixes
- owner: string (required)
- repo: string (required)

## disable_automated_security_fixes
- owner: string (required)
- repo: string (required)
