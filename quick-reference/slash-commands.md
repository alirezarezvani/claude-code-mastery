# Slash Commands

Built-in and custom slash commands for Claude Code.

## Built-in Commands

### Session Management

| Command | Description | When to Use |
|---------|-------------|-------------|
| `/help` | Show all commands | Quick reference |
| `/exit` | Exit Claude Code | End session |
| `/clear` | Clear conversation | Fresh start, polluted context |
| `/compact` | Summarize context | Approaching token limit |
| `/cost` | Show cost & duration | Budget tracking |

### Configuration

| Command | Description | When to Use |
|---------|-------------|-------------|
| `/config` | Open config panel | Change settings |
| `/init` | Create CLAUDE.md | New project setup |
| `/terminal-setup` | Configure terminal | Enable Shift+Enter |
| `/doctor` | Health check | Troubleshooting |

### Session Control

| Command | Description | When to Use |
|---------|-------------|-------------|
| `/memory` | Show CLAUDE.md contents | Verify loaded context |
| `/status` | Show session status | Check context usage |
| `/bug` | Report issue to Anthropic | Found a bug |

### Model & Tools

| Command | Description | When to Use |
|---------|-------------|-------------|
| `/model` | Switch model | Need Opus for complex task |
| `/allowed-tools` | Show allowed tools | Debug permissions |
| `/mcp` | MCP server status | Verify connections |

## Custom Slash Commands

### Creating Project Commands

Location: `.claude/commands/` (shared with team)

**Example: /review command**

`.claude/commands/review.md`:
```markdown
---
description: Review staged changes for issues
---

Review the following staged changes for:
- Security vulnerabilities
- Performance issues
- Code style violations
- Missing error handling

Changes:
!`git diff --staged`

Provide a summary with severity levels (critical/warning/info).
```

**Usage:**
```
/review
```

### Creating Personal Commands

Location: `~/.claude/commands/` (available in all projects)

**Example: /standup command**

`~/.claude/commands/standup.md`:
```markdown
---
description: Generate standup summary
---

Based on my recent git activity, generate a standup summary:

!`git log --oneline --since="yesterday" --author="$(git config user.email)"`

Format:
- Yesterday: [completed items]
- Today: [planned items based on branch/recent changes]
- Blockers: [any failing tests or issues]
```

### Command with Arguments

**Example: /explain command**

`.claude/commands/explain.md`:
```markdown
---
description: Explain a file or concept
---

Explain $ARGUMENTS in detail:
- What it does
- How it works
- Key dependencies
- Potential improvements

If $ARGUMENTS is a file path, analyze @$ARGUMENTS.
```

**Usage:**
```
/explain src/auth/oauth.ts
/explain "the repository pattern"
```

### Advanced Command Examples

**Code Review with Severity:**

`.claude/commands/pr-review.md`:
```markdown
---
description: Comprehensive PR review
model: claude-opus-4-1-20250805
---

Perform a comprehensive code review:

## Changes
!`git diff main...HEAD`

## Review Checklist
- [ ] Security: SQL injection, XSS, auth issues
- [ ] Performance: N+1 queries, unnecessary loops
- [ ] Error handling: Try/catch, validation
- [ ] Types: TypeScript strictness
- [ ] Tests: Coverage for new code

Rate each category: ✅ Pass | ⚠️ Warning | ❌ Fail

Provide specific line-by-line feedback for issues.
```

**Deployment Checklist:**

`.claude/commands/deploy-check.md`:
```markdown
---
description: Pre-deployment verification
---

Pre-deployment checklist:

1. **Tests**: !`npm test 2>&1 | tail -10`
2. **Types**: !`npm run typecheck 2>&1 | tail -10`
3. **Lint**: !`npm run lint 2>&1 | tail -10`
4. **Build**: !`npm run build 2>&1 | tail -10`

Summarize:
- ✅ Ready to deploy
- ⚠️ Warnings to review
- ❌ Blockers to fix
```

## Command Best Practices

### DO

- Use descriptive names: `/review`, `/deploy-check`, `/standup`
- Include clear descriptions in frontmatter
- Use `$ARGUMENTS` for flexible commands
- Specify model for complex commands (Opus for deep analysis)

### DON'T

- Create commands for one-off tasks
- Hardcode project-specific paths in personal commands
- Skip the description — makes `/help` output useless

### Command Organization

```
.claude/commands/
├── review.md           # Code review
├── pr-review.md        # PR-specific review
├── deploy-check.md     # Pre-deployment
├── standup.md          # Daily standup
└── explain.md          # Explain anything
```

---

## Skills vs Commands

| Feature | Slash Commands | Skills |
|---------|---------------|--------|
| **Triggered by** | User types `/command` | Claude decides to use |
| **Location** | `.claude/commands/` | `.claude/skills/` |
| **Use case** | Specific workflows | General capabilities |
| **Arguments** | Via `$ARGUMENTS` | Via skill detection |

**Rule of thumb:** Commands for workflows you trigger. Skills for capabilities Claude should always have.

---

📰 **Related Article:** [Custom Slash Commands for CI/CD Workflows](https://medium.com/@alirezarezvani)
