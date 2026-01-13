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

## Git Workflow & Branching Strategy

**⚠️ IMPORTANT:** We follow a strict Git Flow workflow with mandatory code reviews.

### Quick Start

1. **Always branch from `dev`** (not `main`)
2. **Use branch prefixes:** `feature/`, `fix/`, or `docs/`
3. **Create PR to `dev`** (not `main`)
4. **Wait for code review** (mandatory)
5. **Merge after approval**

### Branch Structure

```
main (production) ← PROTECTED
  └── dev (integration) ← PROTECTED
       ├── feature/your-feature
       ├── fix/bug-name
       └── docs/documentation
```

### Rules
- 🚫 **NEVER** push directly to `main`
- ✅ **ALWAYS** create PRs from feature branches to `dev`
- 📋 **MANDATORY** code review before merging
- 🔍 GitHub App review required (setup instructions to follow)

**→ See [GIT_WORKFLOW.md](./GIT_WORKFLOW.md) for complete workflow documentation**

## Pull Request Process

### 1. Create Your Branch

```bash
# Start from dev
git checkout dev
git pull origin dev

# Create feature branch
git checkout -b feature/add-workflow-example
# OR for fixes
git checkout -b fix/typo-in-readme
# OR for docs
git checkout -b docs/update-contributing
```

### 2. Make Your Changes

- Edit files
- Test any code examples
- Follow the style guide below

### 3. Commit & Push

```bash
git add .
git commit -m "feat: add workflow example

- Clear step-by-step guide
- Includes common scenarios
- Tested in real project

Co-Authored-By: Claude Sonnet 4.5 (1M context) <noreply@anthropic.com>"

git push -u origin feature/add-workflow-example
```

### 4. Create Pull Request

**Target:** `dev` branch (NOT `main`)

```bash
gh pr create --base dev --title "Add workflow example" \
  --body "## Summary
Brief description of changes

## Checklist
- [ ] Tested examples
- [ ] Includes context (when to use / NOT to use)
- [ ] Measured data included (if applicable)
- [ ] Follows style guide"
```

### 5. Code Review

- Wait for automated checks
- Address review feedback
- Get approval from reviewer
- Merge after approval

## Questions?

Open an issue or reach out on [Medium](https://medium.com/@alirezarezvani).

---

**Thank you for helping make this resource better!**
