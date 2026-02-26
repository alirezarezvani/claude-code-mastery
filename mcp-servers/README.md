# MCP Servers

Model Context Protocol servers that extend Claude Code with external integrations.

## What is MCP?

MCP (Model Context Protocol) allows Claude Code to connect to external services like:
- GitHub, Linear, Jira (project management)
- Slack, Discord (communication)
- Databases, APIs (data sources)
- Browser automation (Playwright)

## Configuration

MCP servers are configured in `.mcp.json` at your project root:

```json
{
  "servers": {
    "github": {
      "command": "npx",
      "args": ["@modelcontextprotocol/server-github"]
    },
    "playwright": {
      "type": "sse",
      "url": "https://your-mcp-server.workers.dev/sse"
    }
  }
}
```

## Essential Servers

| Server | Purpose | Status |
|--------|---------|--------|
| **GitHub** | PR, issues, code search | 📋 Config Coming Soon |
| **Playwright** | Browser automation | 📋 Config Coming Soon |
| **Filesystem** | Enhanced file ops | ✅ Built-in |

## Recommended Setup

Configuration examples coming soon. Check the [MCP documentation](https://modelcontextprotocol.io/) for more details.

---

📰 **Related Articles:**
- [Building Custom MCP Servers](https://medium.com/@alirezarezvani)
- [Playwright MCP for Web Testing](https://medium.com/@alirezarezvani)
