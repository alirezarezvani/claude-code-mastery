# My Claude Code Ecosystem

A collection of repositories that extend and complement Claude Code.

## Core Repository

| Repository | Description | Stars |
|------------|-------------|-------|
| **[claude-code-mastery](https://github.com/alirezarezvani/claude-code-mastery)** | This repository — comprehensive reference guide | ⭐ |

## Related Repositories

### Development Tools

| Repository | Description | Use Case |
|------------|-------------|----------|
| [llm-spec-kit](https://github.com/creativerezz/llm-spec-kit) | Spec-driven development toolkit for AI coding agents | Structured development workflow with Claude Code |
| [playwright-mcp-example](https://github.com/creativerezz/playwright-mcp-example) | Playwright MCP server for browser automation | Web testing and automation with Claude Code |

### Coming Soon

| Repository | Description | Status |
|------------|-------------|--------|
| claude-code-skills | Production-ready skill files | 🚧 In Progress |
| claude-code-hooks | Enterprise hook examples | 🚧 In Progress |
| claude-code-workflows | End-to-end workflow templates | 📋 Planned |

## How These Work Together

```
┌─────────────────────────────────────────────────────────────┐
│                   claude-code-mastery                       │
│                 (Reference & Documentation)                 │
└─────────────────────────┬───────────────────────────────────┘
                          │
          ┌───────────────┼───────────────┐
          ▼               ▼               ▼
┌─────────────────┐ ┌─────────────┐ ┌─────────────────┐
│  llm-spec-kit   │ │ playwright- │ │  (future repos) │
│                 │ │ mcp-example │ │                 │
│ Spec-driven     │ │             │ │ Skills, hooks,  │
│ development     │ │ Browser     │ │ workflows       │
│ workflow        │ │ automation  │ │                 │
└─────────────────┘ └─────────────┘ └─────────────────┘
```

## Integration Examples

### Using llm-spec-kit with Claude Code

```bash
# Initialize spec-driven project
npx specify init my-project --ai claude

# Claude Code now has access to /specify, /plan, /constitution commands
claude
> /specify Build a user authentication system with OAuth2
```

### Using Playwright MCP with Claude Code

```json
// .mcp.json
{
  "servers": {
    "playwright": {
      "type": "sse",
      "url": "https://your-playwright-mcp.workers.dev/sse"
    }
  }
}
```

```
claude
> "Navigate to our staging site and take a screenshot of the login page"
[Claude uses Playwright MCP to control browser]
```

## Contributing

Each repository accepts contributions. See individual CONTRIBUTING.md files.

## Support

- **Issues:** Open in the relevant repository
- **Questions:** [GitHub Discussions](https://github.com/alirezarezvani/claude-code-mastery/discussions)
- **Articles:** [Medium @alirezarezvani](https://medium.com/@alirezarezvani)

---

## Full Repository List

### By Topic

**Claude Code:**
- [claude-code-mastery](https://github.com/alirezarezvani/claude-code-mastery) — Reference guide

**AI Development:**
- [llm-spec-kit](https://github.com/creativerezz/llm-spec-kit) — Spec-driven development

**MCP Servers:**
- [playwright-mcp-example](https://github.com/creativerezz/playwright-mcp-example) — Browser automation

---

*Want to see a specific tool or integration? [Open an issue](https://github.com/alirezarezvani/claude-code-mastery/issues) with your suggestion.*
