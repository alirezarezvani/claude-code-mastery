# Claude Code Commands Reference

Complete reference for all Claude Code commands with practical examples and usage notes.

## Starting Claude Code

### Basic Start

```bash
# Interactive mode (most common)
claude

# Start with initial prompt
claude "explain this codebase"

# Start with specific file context
claude "refactor @src/auth.ts for better error handling"
```

### Print Mode (Non-Interactive)

```bash
# Execute and exit — perfect for scripts and CI/CD
claude -p "explain this function"

# Process piped content
cat error.log | claude -p "explain these errors"

# JSON output for parsing
claude -p "list all TODOs" --output-format json
```

**When to use Print Mode:**
- CI/CD pipelines
- Automation scripts
- Quick one-off queries
- Chaining with other tools

**When NOT to use:**
- Multi-turn conversations
- Complex refactoring
- When you need to review before applying changes

### Resume & Continue

```bash
# Resume most recent conversation
claude --resume

# Continue specific session
claude --continue <session-id>
```

## Session Management

### Conversation Control

| Command | Description | When to Use |
|---------|-------------|-------------|
| `/clear` | Clear conversation history | Context is polluted, fresh start needed |
| `/compact` | Summarize and reduce context | Approaching token limit |
| `/cost` | Show session cost & duration | Budget tracking |
| `/exit` | Exit Claude Code | Done with session |

### Context Management

```bash
# Add working directories (multi-repo)
claude --add-dir ../shared-lib ../config

# Reference specific files
claude "refactor @src/auth.ts using patterns from @src/utils.ts"

# Reference multiple files
claude "combine @file1.ts and @file2.ts into a single module"
```

## Model Selection

```bash
# Use Sonnet (default, faster, cheaper)
claude --model sonnet

# Use Opus (complex tasks, deeper reasoning)
claude --model opus

# Specific version
claude --model claude-sonnet-4-20250514
```

### Model Selection Guide

| Model | Best For | Cost | Speed |
|-------|----------|------|-------|
| **Sonnet** | 80% of tasks — daily coding, quick fixes, standard refactors | $ | Fast |
| **Opus** | Complex architecture, deep refactors, subtle bugs | $$$ | Slower |

**My Rule:** Start with Sonnet. Switch to Opus only when Sonnet fails twice on the same task.

## Permission Control

### Allow Specific Tools

```bash
# Allow git commands without prompting
claude --allowedTools "Bash(git log:*)" "Bash(git diff:*)" "Write"

# Allow all npm commands
claude --allowedTools "Bash(npm:*)"
```

### Deny Dangerous Operations

```bash
# Block destructive commands
claude --disallowedTools "Bash(rm -rf:*)" "Bash(sudo:*)"

# Block file reads in sensitive directories
claude --disallowedTools "Read(.env*)" "Read(secrets/**)"
```

### Permission Best Practices

```bash
# Balanced setup for daily development
claude \
  --allowedTools "Bash(git:*)" "Bash(npm run:*)" "Write" "Edit" \
  --disallowedTools "Bash(rm -rf:*)" "Bash(curl:*)" "Read(.env*)"
```

## Output Control

```bash
# JSON output (for parsing)
claude -p "query" --output-format json

# Plain text (default)
claude -p "query" --output-format text

# Streaming JSON (for real-time processing)
claude -p "query" --output-format stream-json
```

## Advanced Options

### Limit Conversation Turns

```bash
# Auto-stop after 3 turns (prevents runaway sessions)
claude -p --max-turns 3 "implement feature X"
```

### Verbose Logging

```bash
# Debug mode — see all tool calls
claude --verbose

# Useful for troubleshooting hooks and skills
```

### Health Check

```bash
# Verify installation and configuration
claude doctor
```

## Special Syntax

### File References

```bash
# Include file content in prompt
claude "explain @src/complex-algorithm.ts"

# Multiple files
claude "compare @old-implementation.ts with @new-implementation.ts"
```

### Inline Bash Execution

```bash
# Run command and include output in context
claude "the tests are failing: !`npm test 2>&1 | tail -20`"

# Get current git status
claude "review my changes: !`git diff --staged`"
```

### URL References

```bash
# Include web content (when web search enabled)
claude "summarize https://docs.example.com/api"
```

## Session Recovery

```bash
# List recent sessions
claude sessions list

# Resume specific session by ID
claude --continue abc123

# Resume last session
claude --resume
```

## Configuration Commands

```bash
# Open config panel
/config

# View current settings
/settings

# Initialize project CLAUDE.md
/init

# Run terminal setup (for Shift+Enter support)
/terminal-setup
```

---

## Common Patterns

### Code Review Workflow

```bash
# Review staged changes
claude "review my staged changes: !`git diff --staged`"

# Or start fresh and load diff
claude
> review @git-diff.txt for security issues
```

### Debug Workflow

```bash
# Pipe error output directly
npm test 2>&1 | claude -p "explain these failures and suggest fixes"

# Or interactive with context
claude "debug this: !`npm test 2>&1 | tail -50`"
```

### Refactoring Workflow

```bash
# Plan first (Ctrl+R enables plan mode)
claude
> [Ctrl+R] # Enable plan mode
> refactor @src/auth/ to use the repository pattern
> [Ctrl+R] # Disable plan mode to execute
```

---

📰 **Related Articles:**
- [The 5 Claude Code Commands Nobody Uses](https://medium.com/@alirezarezvani)
- [Background Tasks: You're Using Ctrl+B Wrong](https://medium.com/@alirezarezvani)
