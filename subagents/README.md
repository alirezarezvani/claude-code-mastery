# Subagents

Custom subagent patterns for specialized tasks.

## What Are Subagents?

Subagents are specialized Claude instances that handle specific tasks. Claude Code can spawn subagents for:
- Code review
- Test generation
- Documentation
- Research

## Available Templates

| Template | Description | Status |
|----------|-------------|--------|
| [Code Reviewer](./templates/code-reviewer.md) | Specialized review agent | 📋 Coming Soon |
| [Test Generator](./templates/test-generator.md) | Generate tests following patterns | 📋 Coming Soon |

## Subagent Patterns

### Basic Subagent

```
"Use a subagent to review this code for security issues"
```

Claude spawns a focused review agent with limited context.

### Custom Subagent

Create in `.claude/agents/`:

```markdown
---
name: security-reviewer
description: Security-focused code review
model: claude-opus-4-1-20250805
---

You are a security-focused code reviewer. Check for:
- SQL injection
- XSS vulnerabilities
- Authentication bypasses
- Sensitive data exposure
```

## Best Practices

### ✅ DO
- Use subagents for focused, specialized tasks
- Give subagents clear, limited scope
- Use appropriate model (Opus for complex analysis)

### ❌ DON'T
- Spawn subagents for simple tasks
- Give subagents access to entire codebase
- Chain too many subagents (context loss)

---

📰 **Related Article:** [Custom Subagents: 90% of Developers Set Them Up Wrong](https://medium.com/@alirezarezvani)
