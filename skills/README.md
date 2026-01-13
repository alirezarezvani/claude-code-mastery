# Claude Code Skills

Production-ready skill files that extend Claude Code's capabilities.

## What Are Skills?

Skills are instruction files that teach Claude Code how to perform specific tasks. Unlike slash commands (which you trigger), skills are automatically activated when Claude determines they're relevant.

## Directory Structure

```
.claude/skills/
├── code-review.md       # Activated for review requests
├── test-writer.md       # Activated for test generation
├── pr-generator.md      # Activated for PR creation
└── doc-generator.md     # Activated for documentation
```

## Available Skills

### Production-Ready

| Skill | Description | Trigger |
|-------|-------------|---------|
| [Code Review](./production-ready/code-review.md) | Comprehensive review checklist | "review", "check for issues" |
| [Test Writer](./production-ready/test-writer.md) | Generate tests following patterns | "write tests", "add tests" |
| [PR Generator](./production-ready/pr-generator.md) | Create detailed PR descriptions | "create PR", "prepare PR" |
| [Doc Generator](./production-ready/doc-generator.md) | Generate documentation | "document", "add docs" |

### Experimental

| Skill | Description | Status |
|-------|-------------|--------|
| [Multi-Agent](./experimental/multi-agent.md) | Coordinate multiple Claude instances | 🧪 Experimental |

## Skill Anatomy

```markdown
---
description: What this skill does (shown in /help)
model: claude-sonnet-4-20250514 (optional override)
user-invocable: true (show in slash menu)
---

# Skill Name

## When to Activate
[Patterns that should trigger this skill]

## Instructions
[Detailed instructions for Claude]

## Output Format
[Expected output structure]
```

## Installation

Copy skill files to `.claude/skills/` in your project:

```bash
mkdir -p .claude/skills
cp path/to/skill.md .claude/skills/
```

## Skills vs Commands vs Hooks

| Feature | Commands | Skills | Hooks |
|---------|----------|--------|-------|
| Triggered by | User types `/command` | Claude decides | Tool execution |
| Location | `.claude/commands/` | `.claude/skills/` | `settings.json` |
| Use case | Explicit workflows | Implicit capabilities | Automation |
| Example | `/review` | Code review knowledge | Auto-format |

---

📰 **Related Article:** [Skills + Hooks: The Claude Code Combo That 5x'd My Output](https://medium.com/@alirezarezvani)
