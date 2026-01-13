# Claude Code Mastery — The Practitioner's Reference

> Production-tested patterns, measured performance data, and honest documentation of what works (and what doesn't) in Claude Code.

[![Medium](https://img.shields.io/badge/Medium-@alirezarezvani-black?style=flat&logo=medium)](https://medium.com/@alirezarezvani)
[![Newsletter](https://img.shields.io/badge/Newsletter-Subscribe-blue?style=flat&logo=substack)](https://your-newsletter-link)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

---

## Why This Repository?

Most Claude Code references tell you **WHAT** commands exist.  
This one tells you **WHEN** to use them, **WHY** they work, and **WHAT** happens when they don't.

### What Makes This Different

| Feature | Other Cheat Sheets | This Repository |
|---------|-------------------|-----------------|
| Commands | ✅ List of commands | ✅ Commands + **when NOT to use them** |
| Examples | ✅ Basic examples | ✅ **Production-tested** patterns with context |
| CLAUDE.md | ✅ Generic template | ✅ **Use-case-specific** templates (solo, team, enterprise) |
| Performance | ❌ Not covered | ✅ **Measured data** — token usage, costs, efficiency |
| Failures | ❌ Not covered | ✅ **Anti-patterns** — what breaks and why |
| Sessions | ❌ Not covered | ✅ **Real transcripts** — annotated production sessions |

---

## Quick Start

### Installation

```bash
# macOS / Linux
curl -fsSL https://claude.ai/install.sh | sh

# Windows (WSL recommended)
irm https://claude.ai/install.ps1 | iex

# Verify installation
claude --version
```

### First Session

```bash
# Navigate to your project
cd your-project

# Start Claude Code
claude

# Or start with a prompt
claude "explain this codebase"
```

### Essential Commands

| Command | Description |
|---------|-------------|
| `/help` | Show all available commands |
| `/init` | Initialize CLAUDE.md in your project |
| `/config` | Open configuration panel |
| `/cost` | Show session cost and token usage |
| `/clear` | Clear conversation history |
| `Ctrl+C` | Cancel current operation |
| `Ctrl+R` | Toggle plan mode (think before acting) |

---

## 📚 Complete Guide

### Core References

| Section | What You'll Learn | Related Article |
|---------|-------------------|-----------------|
| [Quick Reference](./quick-reference/) | Commands, shortcuts, CLI flags | — |
| [CLAUDE.md Templates](./claude-md-templates/) | Use-case-specific configurations | [7 Mistakes Killing Your Agent's Memory](https://medium.com/@alirezarezvani) |
| [Hooks](./hooks/) | Automation, guardrails, enterprise compliance | [Enterprise Hooks: Compliance Without Killing Productivity](https://medium.com/@alirezarezvani) |
| [Skills](./skills/) | Production-ready skill files | [Skills + Hooks: The Combo That 5x'd My Output](https://medium.com/@alirezarezvani) |

### Advanced Topics

| Section | What You'll Learn | Related Article |
|---------|-------------------|-----------------|
| [Performance](./performance/) | Token efficiency, cost optimization, context management | [Why Sessions Die After 10 Minutes](https://medium.com/@alirezarezvani) |
| [Workflows](./workflows/) | End-to-end patterns for real tasks | [Background Tasks: You're Using Ctrl+B Wrong](https://medium.com/@alirezarezvani) |
| [Enterprise](./enterprise/) | Team setup, compliance, audit logging | [Hooks as Enterprise Guardrails](https://medium.com/@alirezarezvani) |
| [Subagents](./subagents/) | Custom subagent patterns | [90% of Developers Set Up Subagents Wrong](https://medium.com/@alirezarezvani) |

### Integrations

| Section | What You'll Learn |
|---------|-------------------|
| [VS Code](./integrations/vscode.md) | VS Code + Claude Code setup |
| [Cursor](./integrations/cursor.md) | Cursor IDE integration |
| [Neovim](./integrations/neovim.md) | Neovim plugin setup |
| [MCP Servers](./mcp-servers/) | Essential MCP server configurations |

---

## 🎯 Start Here (By Experience Level)

### Beginner (< 1 week with Claude Code)

1. Read [Quick Reference → Commands](./quick-reference/commands.md)
2. Copy [CLAUDE.md → Solo Developer](./claude-md-templates/solo-developer.md) to your project
3. Try the [Feature Development Workflow](./workflows/feature-development.md)

### Intermediate (1-4 weeks)

1. Study the [Anti-Patterns](./claude-md-templates/anti-patterns/) — avoid common mistakes
2. Set up [Hooks](./hooks/) for automation
3. Review [Performance → Context Management](./performance/context-management.md)

### Advanced (1+ months)

1. Build [Custom Skills](./skills/production-ready/)
2. Implement [Enterprise Patterns](./enterprise/)
3. Study [Session Transcripts](./workflows/session-transcripts/) for optimization insights

---

## 📊 Measured Insights

Real data from 200+ hours of Claude Code usage:

| Metric | Finding |
|--------|---------|
| **Session lifespan** | Average productive session: 15-25 minutes before context degradation |
| **Token efficiency** | Proper CLAUDE.md reduces token usage by 30-40% |
| **Hook ROI** | Auto-formatting hooks save ~5 min/hour of manual work |
| **Model choice** | Sonnet: 80% of tasks. Opus: complex architecture, deep refactors |
| **Cost optimization** | Background tasks (`Ctrl+B`) reduce interactive token spend by 25% |

*See [Performance](./performance/) for detailed breakdowns and methodology.*

---

## 🔗 My Claude Code Ecosystem

| Repository | Description | Stars |
|------------|-------------|-------|
| **[claude-code-mastery](https://github.com/alirezarezvani/claude-code-mastery)** | This repository — comprehensive reference | ⭐ |
| [llm-spec-kit](https://github.com/creativerezz/llm-spec-kit) | Spec-driven development toolkit | — |
| [playwright-mcp-example](https://github.com/creativerezz/playwright-mcp-example) | Browser automation MCP server | — |

*See [Other Repos](./other-repos/) for the complete ecosystem.*

---

## 📰 Latest Articles

<!-- Keep this section updated with your latest Medium articles -->

| Date | Article | Topic |
|------|---------|-------|
| Jan 2026 | [These 4 Claude Code 2.1 Features Save Me 50+ Minutes Daily](https://medium.com/@alirezarezvani) | Features |
| Jan 2026 | [7 CLAUDE.md Mistakes That Are Killing Your Agent's Memory](https://medium.com/@alirezarezvani) | CLAUDE.md |
| Jan 2026 | [Why Your Claude Code Sessions Die After 10 Minutes](https://medium.com/@alirezarezvani) | Performance |
| Jan 2026 | [Skills + Hooks: The Claude Code Combo That 5x'd My Output](https://medium.com/@alirezarezvani) | Skills |
| Jan 2026 | [Hooks as Enterprise Guardrails: Compliance Without Killing Productivity](https://medium.com/@alirezarezvani) | Enterprise |

*[View all articles →](https://medium.com/@alirezarezvani)*

---

## 🤝 Contributing

Contributions are welcome! Here's how you can help:

- **Fix errors** — Submit a PR for any mistakes you find
- **Add examples** — Share your production-tested patterns
- **Improve docs** — Clarify confusing sections
- **Share data** — Add your measured performance insights

Please read [CONTRIBUTING.md](./CONTRIBUTING.md) before submitting.

---

## 📧 Stay Updated

**Newsletter:** Weekly Claude Code insights, new patterns, and production tips.  
[Subscribe here →](https://your-newsletter-link)

**Medium:** In-depth articles with code examples and measured data.  
[Follow on Medium →](https://medium.com/@alirezarezvani)

---

## License

MIT License — see [LICENSE](./LICENSE) for details.

---

## Acknowledgments

- [Anthropic](https://anthropic.com) for building Claude Code
- The Claude Code community for sharing patterns and insights
- Everyone who contributed feedback and corrections

---

<p align="center">
  <strong>If this repository helped you, please ⭐ star it!</strong><br>
  <em>Built with Claude Code, documented with honesty.</em>
</p>
