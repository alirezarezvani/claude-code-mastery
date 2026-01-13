# CLI Flags Reference

Complete reference for all Claude Code CLI flags and options.

## Basic Flags

| Flag | Short | Description | Example |
|------|-------|-------------|---------|
| `--help` | `-h` | Show help | `claude --help` |
| `--version` | `-v` | Show version | `claude --version` |
| `--verbose` | | Enable debug output | `claude --verbose` |

## Session Flags

| Flag | Description | Example |
|------|-------------|---------|
| `--resume` | Resume last conversation | `claude --resume` |
| `--continue <id>` | Continue specific session | `claude --continue abc123` |

## Model Selection

| Flag | Description | Example |
|------|-------------|---------|
| `--model <name>` | Select model | `claude --model opus` |

**Available Models:**
- `sonnet` — Claude Sonnet (default, faster)
- `opus` — Claude Opus (complex tasks)
- `claude-sonnet-4-20250514` — Specific version
- `claude-opus-4-1-20250805` — Specific version

## Output Flags

| Flag | Description | Example |
|------|-------------|---------|
| `--output-format <fmt>` | Output format | `claude -p "query" --output-format json` |

**Formats:**
- `text` — Plain text (default)
- `json` — JSON with metadata
- `stream-json` — Streaming JSON

## Print Mode

| Flag | Short | Description | Example |
|------|-------|-------------|---------|
| `--print` | `-p` | Non-interactive mode | `claude -p "query"` |
| `--max-turns <n>` | | Limit conversation turns | `claude -p --max-turns 3 "query"` |

**Print Mode Use Cases:**
```bash
# CI/CD automation
claude -p "check for security issues" --output-format json

# Piped input
cat logs.txt | claude -p "summarize errors"

# Script integration
result=$(claude -p "generate function signature for X")
```

## Directory Flags

| Flag | Description | Example |
|------|-------------|---------|
| `--add-dir <paths>` | Add working directories | `claude --add-dir ../lib ../shared` |

**Multi-Repo Pattern:**
```bash
# Work across multiple related repos
claude --add-dir ../api ../web ../shared "refactor auth across all repos"
```

## Permission Flags

| Flag | Description | Example |
|------|-------------|---------|
| `--allowedTools <tools>` | Allow tools without prompt | See below |
| `--disallowedTools <tools>` | Block specific tools | See below |

### Allowed Tools Syntax

```bash
# Allow specific bash commands
claude --allowedTools "Bash(git:*)" "Bash(npm run:*)"

# Allow file operations
claude --allowedTools "Write" "Edit" "Read"

# Allow MCP server tools
claude --allowedTools "mcp__github" "mcp__linear"
```

### Disallowed Tools Syntax

```bash
# Block destructive commands
claude --disallowedTools "Bash(rm -rf:*)" "Bash(sudo:*)"

# Block sensitive file reads
claude --disallowedTools "Read(.env*)" "Read(secrets/**)"
```

### Production Setup Example

```bash
claude \
  --allowedTools \
    "Bash(git:*)" \
    "Bash(npm run:*)" \
    "Bash(npm test:*)" \
    "Write" \
    "Edit" \
  --disallowedTools \
    "Bash(rm -rf:*)" \
    "Bash(curl:*)" \
    "Bash(wget:*)" \
    "Read(.env*)" \
    "Read(**/secrets/**)"
```

## Input Flags

| Flag | Description | Example |
|------|-------------|---------|
| `--input-format <fmt>` | Input format | `claude -p --input-format stream-json` |

**Formats:**
- `text` — Plain text (default)
- `stream-json` — JSON stream input

## Configuration Flags

| Flag | Description | Example |
|------|-------------|---------|
| `--config <path>` | Custom config file | `claude --config ./custom-settings.json` |

## Update Flag

| Flag | Description | Example |
|------|-------------|---------|
| `update` | Update Claude Code | `claude update` |

## Common Flag Combinations

### Daily Development

```bash
# Standard development session with git permissions
claude --allowedTools "Bash(git:*)" "Write" "Edit"
```

### Code Review (Read-Only)

```bash
# Review without modification permissions
claude --disallowedTools "Write" "Edit" "Bash(*)"
```

### CI/CD Integration

```bash
# Non-interactive with JSON output
claude -p \
  --output-format json \
  --max-turns 1 \
  "analyze security of staged changes"
```

### Multi-Repo Work

```bash
# Work across monorepo packages
claude \
  --add-dir packages/api packages/web packages/shared \
  "ensure consistent error handling across all packages"
```

### Deep Analysis (Opus)

```bash
# Complex task with Opus
claude \
  --model opus \
  --allowedTools "Read" \
  --disallowedTools "Write" "Edit" \
  "analyze architecture and suggest improvements"
```

## Environment Variables

| Variable | Description |
|----------|-------------|
| `ANTHROPIC_API_KEY` | API key (if not using subscription) |
| `CLAUDE_CODE_USE_BEDROCK` | Use AWS Bedrock |
| `ANTHROPIC_BEDROCK_BASE_URL` | Bedrock endpoint |

---

## Flag Precedence

1. CLI flags override config file settings
2. Project `.claude/settings.json` overrides user `~/.claude/settings.json`
3. `--disallowedTools` takes precedence over `--allowedTools`

---

📰 **Related Article:** [Claude Permissions & Auto-Accept: The Security Tradeoff](https://medium.com/@alirezarezvani)
