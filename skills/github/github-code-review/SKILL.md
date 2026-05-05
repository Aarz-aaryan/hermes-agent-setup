# GitHub Code Review — Review PRs with Inline Comments

## About
Tools for reviewing GitHub pull requests using the REST API (preferred) or GraphQL (for large diffs).

## Workflow
1. `GITHUB_SEARCH_PULL_REQUESTS` to find the PR
2. `GITHUB_GET_A_PULL_REQUEST` to get full PR details including diff URL
3. `GITHUB_GET_PULL_REQUEST_FILES` or `GITHUB_LIST_PULL_REQUESTS_FILES` for changed files
4. For inline comments: `GITHUB_CREATE_A_PULL_REQUEST_REVIEW_COMMENT` or `GITHUB_CREATE_A_PULL_REQUEST_REVIEW`
5. For large diffs: use GraphQL `github_pull_request_graphql` (handles pagination automatically)

## search_pull_requests
- owner: string (required)
- repo: string (required)
- query: string (required)
- sort: 'created' | 'updated' | 'popularity' | 'long-running' (default 'created')
- order: 'asc' | 'desc' (default 'desc')
- per_page: number (default 30, max 100)
- page: number (default 1)

Query syntax examples:
- `is:pr is:open` — open PRs
- `is:pr is:closed` — closed PRs
- `is:pr is:merged` — merged PRs
- `is:pr author:username` — PRs by user
- `is:pr review:approved` — approved PRs
- `is:pr review:required` — PRs requiring review
- `is:pr head:branch-name` — PRs from a branch
- `is:pr base:branch-name` — PRs targeting a branch

## get_a_pull_request
- owner: string (required)
- repo: string (required)
- pull_number: number (required)

## list_pull_requests_files
- owner: string (required)
- repo: string (required)
- pull_number: number (required)
- per_page: number (default 30, max 100)
- page: number (default 1)

## get_pull_request_files
- owner: string (required)
- repo: string (required)
- pull_number: number (required)
- per_page: number (default 30, max 100)
- page: number (default 1)

## get_a_pull_request_review
- owner: string (required)
- repo: string (required)
- pull_number: number (required)
- review_id: number (required)

## list_pull_request_reviews
- owner: string (required)
- repo: string (required)
- pull_number: number (required)
- per_page: number (default 30, max 100)
- page: number (default 1)

## create_a_pull_request_review_comment
- owner: string (required)
- repo: string (required)
- pull_number: number (required)
- body: string (required)
- commit_id: string (optional)
- path: string (optional)
- line: number (optional — line in the diff)
- start_line: number (optional)
- side: 'LEFT' | 'RIGHT' (optional)
- start_side: 'LEFT' | 'RIGHT' | 'side' (optional)
- in_reply_to: number (optional — comment ID to reply to)

## create_a_pull_request_review
- owner: string (required)
- repo: string (required)
- pull_number: number (required)
- event: 'APPROVE' | 'REQUEST_CHANGES' | 'COMMENT' (required)
- body: string (optional)
- comments: array of { path, body, line, side, start_line, start_side, in_reply_to } (optional)
- commit_id: string (optional)

## create_issue_comment (fallback for PR comments)
- owner: string (required)
- repo: string (required)
- issue_number: number (required — same as PR number)
- body: string (required)

## github_pull_request_graphql
### query
```
query {
  repository(owner: "owner", name: "repo") {
    pullRequest(number: N) {
      title
      body
      state
      url
      changedFiles
      files(first: 100) {
        nodes { path, additions, deletions, changeType }
        pageInfo { hasNextPage, endCursor }
      }
      commits(last: 1) {
        nodes {
          commit { oid, message, statusCheckRollup { state } }
        }
      }
      reviews(last: 10) {
        nodes { author { login }, state, body, submittedAt }
      }
      reviewThreads(first: 50) {
        nodes { id, isResolved, comments(first: 50) {
          nodes { body, path, line, DiffSide(databaseId: true)
            author { login }
          }
        }}
      }
    }
  }
}
```

### Review Comments via GraphQL
```
mutation {
  addPullRequestReviewThread(input: {
    pullRequestReviewId: "review_id",
    body: "comment body",
    filePath: "path/to/file.js",
    line: 42,
    side: RIGHT
  }) { thread { id } }
}
```

## get_the_combined_status_of_a_reference
- owner: string (required)
- repo: string (required)
- ref: string (required — branch or commit SHA)

## list_status_check_contexts_for_a_reference
- owner: string (required)
- repo: string (required)
- ref: string (required)
