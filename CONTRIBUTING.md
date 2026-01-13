# Contributing to Claude Code Mastery

Thank you for your interest in contributing! This repository aims to be the most practical, honest Claude Code reference available.

## How to Contribute

### 1. Fix Errors

Found a mistake? Please submit a PR with:
- The correction
- A brief explanation of why it was wrong
- Source/reference if applicable

### 2. Add Examples

Share your production-tested patterns:
- Must be tested in real projects (not theoretical)
- Include context: when to use, when NOT to use
- Add any measured data if available

### 3. Improve Documentation

Help clarify confusing sections:
- Explain concepts more clearly
- Add diagrams or visual aids
- Improve code formatting

### 4. Share Performance Data

Add your measured insights:
- Token usage patterns
- Session cost data
- Efficiency metrics
- Include your methodology

## Contribution Guidelines

### Code Examples

```markdown
# Good: Includes context and caveats
This hook auto-formats code after edits:
\`\`\`json
{
  "hooks": {
    "PostToolUse": [...]
  }
}
\`\`\`
**When to use:** Projects with strict formatting requirements
**When NOT to use:** Large files (>1000 lines) — causes noticeable delay

# Bad: Just code without context
\`\`\`json
{
  "hooks": {...}
}
\`\`\`
```

### Writing Style

- **Be honest** — Document failures and limitations
- **Be specific** — "Reduces token usage by ~30%" not "improves performance"
- **Be practical** — Focus on real-world usage
- **Avoid marketing speak** — No "revolutionary" or "game-changing"

### File Naming

- Use lowercase with hyphens: `context-management.md`
- Be descriptive: `auto-format-hook.json` not `hook1.json`

## Pull Request Process

1. Fork the repository
2. Create a feature branch: `git checkout -b add-workflow-example`
3. Make your changes
4. Test any code examples
5. Submit PR with clear description

## Questions?

Open an issue or reach out on [Medium](https://medium.com/@alirezarezvani).

---

**Thank you for helping make this resource better!**
