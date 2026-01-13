# CLAUDE.md Templates

Use-case-specific CLAUDE.md templates that actually work in production.

## Why CLAUDE.md Matters

CLAUDE.md is Claude Code's memory file. A well-crafted CLAUDE.md:
- **Reduces token usage by 30-40%** — Claude doesn't re-discover your patterns
- **Improves consistency** — Same approach across sessions
- **Prevents mistakes** — Documents what NOT to do
- **Speeds up onboarding** — New team members inherit context

## Templates by Use Case

| Template | Best For | Complexity |
|----------|----------|------------|
| [Solo Developer](./solo-developer.md) | Personal projects, quick iterations | Simple |
| [Team Project](./team-project.md) | Collaborative development | Medium |
| [Enterprise Compliance](./enterprise-compliance.md) | Regulated industries, audits | Complex |
| [Open Source Maintainer](./open-source-maintainer.md) | Community contributions | Medium |
| [Monorepo](./monorepo.md) | Multi-package repositories | Complex |

## Template Structure

Every effective CLAUDE.md has these sections:

```markdown
# Project Overview
Brief context — what is this project?

# Tech Stack
Languages, frameworks, key dependencies

# Development Commands
Build, test, lint — the commands Claude should use

# Code Patterns
How YOU write code in this project

# Constraints
What Claude should NEVER do

# File Structure
Where things live
```

## Quick Start

1. Choose the template closest to your use case
2. Copy to your project root as `CLAUDE.md`
3. Customize the sections (especially Commands and Patterns)
4. Run `/memory` in Claude Code to verify it loaded

## Anti-Patterns

See [Anti-Patterns](./anti-patterns/) for common mistakes:
- [7 CLAUDE.md Mistakes](./anti-patterns/common-mistakes.md)

---

## Template Comparison

| Feature | Solo | Team | Enterprise | OSS | Monorepo |
|---------|------|------|------------|-----|----------|
| Minimal setup | ✅ | | | | |
| Code ownership | | ✅ | ✅ | | ✅ |
| Compliance rules | | | ✅ | | |
| Contribution guidelines | | | | ✅ | |
| Cross-package context | | | | | ✅ |
| Lines of config | ~50 | ~100 | ~200 | ~120 | ~150 |

---

📰 **Related Article:** [7 CLAUDE.md Mistakes That Are Killing Your Agent's Memory](https://medium.com/@alirezarezvani)
