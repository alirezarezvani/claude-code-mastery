# Workflows

End-to-end patterns for common development tasks with Claude Code.

## Available Workflows

| Workflow | Description | Complexity | Status |
|----------|-------------|------------|--------|
| **Feature Development** | Full cycle: plan → implement → test → PR | Medium | 📋 Coming Soon |
| **Bug Investigation** | Systematic debugging approach | Medium | 📋 Coming Soon |
| **Code Review** | PR review workflow | Simple | 📋 Coming Soon |
| **Refactoring** | Safe refactor patterns | Complex | 📋 Coming Soon |

## Session Transcripts

Real annotated sessions showing Claude Code in action:

| Transcript | What It Shows | Status |
|------------|---------------|--------|
| **Successful Refactor** | Auth module refactor — what went right | 📋 Coming Soon |
| **Failed Migration** | Database migration — what went wrong | 📋 Coming Soon |

## Quick Workflow Reference

### Feature Development (15-30 min)

```
1. Plan Mode On          [Ctrl+R]
2. Describe feature      "Add user export feature to admin panel"
3. Review plan           [Verify approach before implementation]
4. Plan Mode Off         [Ctrl+R]
5. Implement             [Claude writes code]
6. Test                  "Run tests for the new feature"
7. Review                "Review changes for issues"
8. Commit                "Create commit with conventional message"
```

### Bug Fix (10-20 min)

```
1. Share context         "Bug: users can't login. Error: !`cat error.log | tail -20`"
2. Investigate           [Claude analyzes]
3. Identify root cause   [Claude explains]
4. Fix                   "Fix the root cause"
5. Verify                "Run tests to verify fix"
6. Commit                "Commit with fix message"
```

### Code Review (5-10 min)

```
1. Load diff             "Review staged changes: !`git diff --staged`"
2. Get feedback          [Claude reviews]
3. Address issues        "Fix the issues you identified"
4. Re-review             "Verify fixes"
```

### Refactoring (20-45 min)

```
1. Plan Mode On          [Ctrl+R]
2. Explain goal          "Refactor @src/auth/ to use repository pattern"
3. Get plan              [Claude creates detailed plan]
4. Checkpoint            [Git commit current state]
5. Plan Mode Off         [Ctrl+R]
6. Execute in phases     [One module at a time]
7. Test after each       "Run tests"
8. Commit each phase     [Incremental commits]
```

## Workflow Principles

### 1. Always Plan Complex Changes

```
[Ctrl+R] → Plan mode on
"I want to add caching to the API layer"
[Claude thinks, creates plan]
[You review plan]
[Ctrl+R] → Plan mode off
[Claude executes plan]
```

**Why:** Prevents wasted tokens on wrong approaches.

### 2. Checkpoint Before Risk

```
"We're about to modify the database schema. Let me commit current state first."
> "Create a checkpoint commit"
[Safe to proceed]
```

**Why:** Easy rollback if something breaks.

### 3. Test After Changes

```
[Claude makes changes]
"Run relevant tests"
[Tests pass] → Continue
[Tests fail] → Fix before moving on
```

**Why:** Catch issues early, not after 10 more changes.

### 4. Commit Incrementally

```
# NOT: One massive commit at the end
# YES: Commit after each logical unit

"Commit: Add repository interface"
"Commit: Implement user repository"  
"Commit: Migrate auth service to use repository"
```

**Why:** Easier to review, debug, and rollback.

---

📰 **Related Articles:**
- [Background Tasks: You're Using Ctrl+B Wrong](https://medium.com/@alirezarezvani)
- [Plan Mode Deep Dive: When It Helps vs When It Hurts](https://medium.com/@alirezarezvani)
