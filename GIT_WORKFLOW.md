# Git Workflow & Branching Strategy

## Branch Structure

This repository follows a **Git Flow** branching model with strict code review requirements.

```
main (production)
  └── dev (integration)
       ├── feature/feature-name
       ├── fix/bug-name
       └── docs/documentation-update
```

### Branch Descriptions

| Branch | Purpose | Protected | Merges From | Merges To |
|--------|---------|-----------|-------------|-----------|
| **main** | Production-ready code | ✅ Yes | `dev` only | Never |
| **dev** | Integration branch | ✅ Yes | feature/fix/docs branches | `main` |
| **feature/** | New features | ❌ No | `dev` | `dev` |
| **fix/** | Bug fixes | ❌ No | `dev` | `dev` |
| **docs/** | Documentation only | ❌ No | `dev` | `dev` |

---

## Workflow Rules

### 🚫 **NEVER** Push Directly to Main
- All changes MUST go through `dev` first
- `main` only receives merges from `dev` after comprehensive review
- Direct commits to `main` are blocked

### ✅ **ALWAYS** Use Feature Branches
- Create branches from `dev`, not `main`
- Use descriptive branch names with prefixes
- Delete branches after merging

### 📋 **MANDATORY** Code Reviews
- Every PR requires at least one approval
- Code review is conducted via GitHub App (details below)
- No self-merging allowed

---

## Step-by-Step Workflow

### 1. Starting New Work

```bash
# Ensure you're on dev and it's up to date
git checkout dev
git pull origin dev

# Create a new feature branch
git checkout -b feature/add-performance-guide

# OR for bug fixes
git checkout -b fix/typo-in-readme

# OR for documentation
git checkout -b docs/update-contributing-guide
```

### 2. Making Changes

```bash
# Make your changes
# ...

# Stage and commit
git add .
git commit -m "Add comprehensive performance optimization guide

- Context management strategies
- Token efficiency patterns
- Cost reduction techniques
- Measured data from production usage

Co-Authored-By: Claude Sonnet 4.5 (1M context) <noreply@anthropic.com>"

# Push to remote
git push -u origin feature/add-performance-guide
```

### 3. Creating Pull Request

```bash
# Open PR from your branch to dev (NOT main)
# Use GitHub CLI or web interface
gh pr create --base dev --head feature/add-performance-guide \
  --title "Add performance optimization guide" \
  --body "## Summary
- New performance guide covering context management
- Token efficiency patterns with measured data
- Production-tested cost reduction techniques

## Checklist
- [x] Tested examples
- [x] Includes context (when to use / when NOT to use)
- [x] Measured data included
- [x] Follows style guide"
```

### 4. Code Review Process

1. **Automated Checks** (if configured)
   - Markdown linting
   - Link validation
   - File naming conventions

2. **Manual Review** (via GitHub App - setup required)
   - Content accuracy
   - Code example quality
   - Documentation clarity
   - Style guide compliance

3. **Address Feedback**
   ```bash
   # Make requested changes
   git add .
   git commit -m "Address review feedback: clarify token efficiency section"
   git push
   ```

4. **Approval & Merge**
   - Once approved, merge into `dev`
   - Delete feature branch after merge

### 5. Releasing to Main

```bash
# Periodic releases from dev to main
# Only after comprehensive testing and review

# Create PR from dev to main
git checkout dev
git pull origin dev

gh pr create --base main --head dev \
  --title "Release: Week of Jan 13, 2026" \
  --body "## Changes in This Release

### New Features
- Performance optimization guide
- Advanced hooks examples
- Enterprise compliance patterns

### Bug Fixes
- Fixed typos in quick reference
- Corrected CLI flag documentation

### Documentation
- Updated CONTRIBUTING.md
- Added Git workflow guide

## Review Checklist
- [x] All PRs to dev have been reviewed
- [x] No breaking changes
- [x] Documentation is up to date
- [x] Examples are tested"
```

---

## Branch Naming Conventions

### Feature Branches
```
feature/add-mcp-examples
feature/playwright-integration
feature/custom-hooks-guide
```

### Fix Branches
```
fix/typo-in-quick-reference
fix/broken-link-in-readme
fix/incorrect-cli-flag
```

### Documentation Branches
```
docs/update-contributing
docs/add-workflow-guide
docs/clarify-hooks-section
```

### Naming Rules
- Use lowercase with hyphens
- Be descriptive but concise
- Include ticket number if applicable: `feature/gh-42-add-examples`

---

## Commit Message Guidelines

### Format
```
<type>: <subject>

<body>

<footer>
```

### Types
- **feat:** New feature
- **fix:** Bug fix
- **docs:** Documentation only
- **refactor:** Code restructuring
- **test:** Adding tests
- **chore:** Maintenance tasks

### Examples

**Good:**
```
feat: Add enterprise compliance CLAUDE.md template

- HIPAA, SOC 2, PCI-DSS patterns
- Audit logging configuration
- Sensitive data handling guidelines
- Tested in regulated environment

Co-Authored-By: Claude Sonnet 4.5 (1M context) <noreply@anthropic.com>
```

**Bad:**
```
update stuff
```

---

## Branch Protection Rules

### Recommended GitHub Settings

#### For `main` branch:
- ✅ Require pull request reviews (1+ approvals)
- ✅ Require status checks to pass
- ✅ Require branches to be up to date
- ✅ Require conversation resolution
- ✅ Restrict who can push (disable direct pushes)
- ✅ Do not allow bypassing settings

#### For `dev` branch:
- ✅ Require pull request reviews (1+ approvals)
- ✅ Require status checks to pass
- ⚠️ Optional: Require branches to be up to date
- ✅ Require conversation resolution

#### Setup Instructions:
1. Go to GitHub repository → Settings → Branches
2. Add branch protection rule for `main`
3. Add branch protection rule for `dev`
4. Configure settings as above

---

## GitHub App Integration

### Code Review Automation

**Status:** To be configured after installing GitHub App

The GitHub App will provide:
- Automated code review
- Style guide enforcement
- Link validation
- Content quality checks
- Performance impact analysis

**Setup Steps:** (Details to follow)
1. Install GitHub App on repository
2. Configure review rules
3. Set up CI/CD pipeline
4. Enable automatic checks

---

## Common Scenarios

### Scenario 1: Hotfix to Production

Even hotfixes follow the workflow:
```bash
git checkout dev
git pull origin dev
git checkout -b fix/critical-security-issue

# Make fix
git add .
git commit -m "fix: patch XSS vulnerability in example code"
git push -u origin fix/critical-security-issue

# Create PR to dev → get review → merge to dev
# Then create PR from dev to main → merge
```

### Scenario 2: Multiple Features in Parallel

```bash
# Developer A
git checkout -b feature/add-vim-integration
# Work on vim integration...

# Developer B
git checkout dev
git checkout -b feature/add-performance-metrics
# Work on metrics...

# Both merge to dev independently
# Conflicts resolved during PR review
```

### Scenario 3: Syncing with Latest Dev

```bash
# Update your feature branch with latest dev
git checkout feature/my-feature
git fetch origin dev
git merge origin/dev

# OR use rebase for cleaner history
git rebase origin/dev

# Resolve conflicts if any, then push
git push --force-with-lease  # if rebased
```

---

## Best Practices

### ✅ DO
- Create small, focused PRs
- Write descriptive commit messages
- Keep feature branches short-lived (< 1 week)
- Pull latest `dev` before starting new work
- Delete branches after merging
- Request reviews promptly

### ❌ DON'T
- Push directly to `main` or `dev`
- Create long-lived feature branches
- Merge without review
- Self-approve PRs
- Force push to shared branches (except with --force-with-lease)
- Commit untested code

---

## Questions?

- Open an issue for workflow questions
- Reach out on [Medium](https://medium.com/@alirezarezvani)
- Check GitHub Discussions for community support

---

**This workflow ensures code quality, maintains project integrity, and enables collaborative development at scale.**
