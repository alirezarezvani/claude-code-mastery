# Claude Code Hooks

Automate tasks, enforce guardrails, and extend Claude Code with hooks.

## What Are Hooks?

Hooks are shell commands that run automatically at specific points in Claude Code's workflow:

| Hook Type | When It Runs | Use Cases |
|-----------|--------------|-----------|
| `PreToolUse` | Before a tool executes | Validation, security checks |
| `PostToolUse` | After a tool executes | Formatting, logging, notifications |
| `Stop` | When Claude completes | Activity logging, cleanup |

## Hook Configuration

Hooks live in `.claude/settings.json`:

```json
{
  "hooks": {
    "PreToolUse": [...],
    "PostToolUse": [...],
    "Stop": [...]
  }
}
```

## Available Examples

| Example | Description | Complexity |
|---------|-------------|------------|
| [Auto-Format](./examples/auto-format.json) | Format code after edits | Simple |
| [Activity Logger](./examples/activity-logger.json) | Log all sessions | Simple |
| [Security Audit](./examples/security-audit.json) | Block dangerous operations | Medium |
| [Enterprise Guardrails](./examples/enterprise-guardrails.json) | Compliance enforcement | Complex |

## Quick Start

### 1. Auto-Format Hook (Most Common)

Add to `.claude/settings.json`:

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "npx prettier --write \"$CLAUDE_FILE_PATH\""
          }
        ]
      }
    ]
  }
}
```

### 2. Activity Logger

```json
{
  "hooks": {
    "Stop": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "echo \"$(date): $CLAUDE_CONVERSATION_SUMMARY\" >> ~/.claude/activity.log"
          }
        ]
      }
    ]
  }
}
```

## Hook Variables

| Variable | Description | Available In |
|----------|-------------|--------------|
| `$CLAUDE_FILE_PATH` | File being modified | PostToolUse (Edit/Write) |
| `$CLAUDE_TOOL_NAME` | Tool being used | All hooks |
| `$CLAUDE_PROJECT_DIR` | Project root directory | All hooks |
| `$CLAUDE_CONVERSATION_SUMMARY` | Session summary | Stop hook |

## Matchers

Matchers filter which tools trigger the hook:

```json
// Match specific tools
"matcher": "Edit"
"matcher": "Write"
"matcher": "Edit|Write"
"matcher": "Bash"

// Match all tools
"matcher": "*"
```

## Best Practices

### DO
- Test hooks manually before adding
- Use absolute paths or `$CLAUDE_PROJECT_DIR`
- Keep hooks fast (< 2 seconds)
- Log hook failures for debugging

### DON'T
- Run expensive operations in PreToolUse (blocks Claude)
- Modify files in PreToolUse (causes conflicts)
- Skip error handling in hook scripts

## Performance Impact

| Hook Type | Impact | Recommendation |
|-----------|--------|----------------|
| PreToolUse | Blocks until complete | Keep < 500ms |
| PostToolUse | Runs after tool | Keep < 2s |
| Stop | Runs at end | Can be longer |

---

📰 **Related Articles:**
- [Skills + Hooks: The Claude Code Combo That 5x'd My Output](https://medium.com/@alirezarezvani)
- [Hooks as Enterprise Guardrails](https://medium.com/@alirezarezvani)
