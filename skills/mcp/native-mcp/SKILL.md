# Native MCP — Connect MCP Servers, Register Tools

## Concept
The Hermes MCP client lets you connect any MCP server (stdio or HTTP) and expose its tools directly to agents. Configure servers in `config.yaml`.

## Config

```yaml
mcp_servers:
  my-server:
    url: https://example.com/mcp  # HTTP MCP server
    headers:
      Authorization: Bearer token
  local-server:
    command: /path/to/server
    args:
      - --verbose
    env:
      MY_VAR: value
  stdio-server:
    command: node
    args:
      - /path/to/server.js
```

## Connection Types

### HTTP (Remote) MCP Servers
```yaml
mcp_servers:
  composio:
    url: https://connect.composio.dev/mcp
    headers:
      x-consumer-api-key: YOUR_API_KEY
    timeout: 180
```

### Local Stdio Servers
```yaml
mcp_servers:
  filesystem:
    command: npx
    args:
      - -y
      - @modelcontextprotocol/server-filesystem
      - /path/to/allowed/dir
    env:
     坡   # Optional env vars
```

### Custom Executable
```yaml
mcp_servers:
  custom:
    command: /path/to/mcp-server
    args:
      - --option
    env:
      API_KEY: secret
    timeout: 60
```

## Auto-start
Servers with `command` are auto-started when Hermes starts. HTTP servers are always-on.

## Stdio Server Lifecycle
Hermes manages the server process — starts on first tool call, restarts if it crashes (max 3 retries), stops when Hermes exits.

## Known MCP Servers
- `composio` — Composio MCP (SaaS integrations)
- `@modelcontextprotocol/server-filesystem` — filesystem access
- `@modelcontextprotocol/server-github` — GitHub
- `@modelcontextprotocol/server-slack` — Slack
- `@modelcontextprotocol/server-brave-search` — Brave search
- `@modelcontextprotocol/server-memory` — persistent memory

## HTTP Server Timeouts
Set per-server timeout (in seconds):
```yaml
mcp_servers:
  slow-server:
    url: https://example.com/mcp
    timeout: 300
```

## Error Handling
If an MCP tool fails:
1. Check server is running: `ps aux | grep mcp`
2. Check logs: Hermes logs MCP traffic at DEBUG level
3. Restart server: kill the process and the next tool call will restart it
4. If server is consistently failing, remove from config

## Security
- Only connect to servers you trust
- Use HTTPS for remote servers
- Don't expose sensitive env vars in server configs
- Audit server capabilities before connecting
