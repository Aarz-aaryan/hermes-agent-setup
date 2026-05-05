---
name: airtable
description: "Airtable: manage bases, tables, records via API."
version: 1.0.0
---

# Airtable

Manage Airtable bases, tables, and records.

## Setup

```yaml
mcp_servers:
  airtable:
    command: npx
    args: ["-y", "@modelcontextprotocol/server-airtable"]
    env:
      AIRTABLE_API_KEY: YOUR_API_KEY
```

## Operations

- List bases and tables
- Create/update/delete records
- Query with filters
