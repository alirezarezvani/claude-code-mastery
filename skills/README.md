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

| Skill | Description | Trigger | Status |
|-------|-------------|---------|--------|
| **Code Review** | Comprehensive review checklist | "review", "check for issues" | 📋 Coming Soon |
| **Test Writer** | Generate tests following patterns | "write tests", "add tests" | 📋 Coming Soon |
| **PR Generator** | Create detailed PR descriptions | "create PR", "prepare PR" | 📋 Coming Soon |
| **Doc Generator** | Generate documentation | "document", "add docs" | 📋 Coming Soon |

### Experimental

| Skill | Description | Status |
|-------|-------------|--------|
| **Multi-Agent** | Coordinate multiple Claude instances | 📋 Experimental (Coming Soon) |

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
