# Keyboard Shortcuts

Platform-specific keyboard shortcuts for Claude Code efficiency.

## Universal Shortcuts

| Shortcut | Action | Notes |
|----------|--------|-------|
| `Ctrl+C` | Cancel current operation | Stops generation mid-stream |
| `Ctrl+D` | Exit Claude Code | Same as `/exit` |
| `Tab` | Auto-complete | Commands, file paths |
| `Up/Down` | Navigate history | Cycle through previous prompts |
| `Ctrl+L` | Clear terminal | Visual cleanup only, keeps context |

## Plan Mode

| Shortcut | Action | When to Use |
|----------|--------|-------------|
| `Ctrl+R` | Toggle plan mode | Before complex changes — Claude thinks first |
| `Shift+Tab` (2x) | Quick read-only mode | Research without modifying files |

**Plan Mode Insight:** Use for refactors touching 3+ files. Overhead not worth it for single-file changes.

## Background Tasks

| Shortcut | Action | When to Use |
|----------|--------|-------------|
| `Ctrl+B` | Send to background | Long-running tasks, continue working |
| `Ctrl+O` | Open transcript view | Monitor background task progress |

**Background Task Pattern:**
```
You: "run full test suite and summarize failures"
[Ctrl+B] → task runs in background
[continue working on other prompts]
[Ctrl+O] → check progress
```

## Input Shortcuts

| Shortcut | Action | Notes |
|----------|--------|-------|
| `Shift+Enter` | Submit message | Requires `/terminal-setup` first |
| `\ + Enter` | Submit (fallback) | Works if Shift+Enter fails |
| `Ctrl+U` | Clear current input | Start fresh |
| `Ctrl+W` | Delete word | Quick editing |

### Setting Up Shift+Enter

Run this in Claude Code:
```
/terminal-setup
```

Or manual setup for iTerm2:
1. Preferences → Profiles → Keys
2. Add: Shift+Enter → Send Escape Sequence → `[13;2u`

## File Navigation

| Shortcut | Action |
|----------|--------|
| `@` + filename | Reference file in prompt |
| `!` + backticks | Execute command, include output |

## IDE Integration Shortcuts

### VS Code / Cursor

| Shortcut | Action |
|----------|--------|
| `Cmd/Ctrl+Shift+C` | New terminal |
| `Cmd/Ctrl+J` | Toggle terminal panel |
| `Cmd/Ctrl+1/2/3` | Switch editor panes |

### Terminal Navigation

| Shortcut | Action |
|----------|--------|
| `Cmd/Ctrl+Shift+[` | Previous terminal |
| `Cmd/Ctrl+Shift+]` | Next terminal |

## Efficiency Patterns

### Quick Code Review

```
[in terminal]
git diff --staged > /tmp/changes.diff
claude "review @/tmp/changes.diff"
```

### Parallel Sessions

```bash
# Terminal 1: Main development
claude

# Terminal 2: Background research (Ctrl+B not needed)
claude -p "research best practices for X"
```

### Keyboard-First Workflow

1. `Cmd+J` → Open terminal
2. `claude` → Start session
3. Type prompt → `Shift+Enter` to submit
4. `Ctrl+R` → Plan mode for complex tasks
5. `Ctrl+B` → Background for long tasks
6. `Ctrl+C` → Cancel if going wrong
7. `Ctrl+D` → Exit when done

---

## Troubleshooting

### Shift+Enter Not Working?

1. Run `/terminal-setup` in Claude Code
2. Restart your terminal
3. If still failing, use `\ + Enter` as fallback

### Ctrl+R Not Toggling Plan Mode?

- Check if terminal is capturing the shortcut
- Try in a fresh terminal session
- Some terminals use Ctrl+R for history search — rebind if needed

---

📰 **Related Article:** [Background Tasks: You're Using Ctrl+B Wrong](https://medium.com/@alirezarezvani)
