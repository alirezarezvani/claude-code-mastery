# Context Management

Why Claude Code sessions degrade and how to prevent it.

## The Problem

After 10-20 minutes of complex work, you notice:
- Claude repeats suggestions you already rejected
- It forgets decisions made earlier in the session
- Responses become less accurate
- It asks questions you already answered

**This isn't a bug — it's context window limits.**

## How Context Works

Claude Code has a finite context window (~200k tokens). Every message consumes context:

| Content Type | Token Cost | Accumulation |
|--------------|-----------|--------------|
| Your prompts | ~50-200 per message | Linear |
| Claude's responses | ~200-2000 per response | Linear |
| File contents (@file) | ~1 token per 4 chars | Each reference |
| Tool outputs | ~100-500 per tool | Linear |
| CLAUDE.md | Fixed cost at start | One-time |

## Warning Signs

| Context Usage | Symptoms | Action |
|---------------|----------|--------|
| < 50% | Normal operation | Continue |
| 50-70% | Slight degradation possible | Monitor |
| 70-85% | Noticeable issues | Use `/compact` |
| > 85% | Severe degradation | New session or `/compact` |

## Prevention Strategies

### 1. Monitor Context Usage

```
/cost
```

Check the context percentage regularly during long sessions.

### 2. Use /compact Proactively

Don't wait for degradation:

```
[Context at 70%]
/compact

Claude summarizes the conversation and continues with fresh context.
```

### 3. Scope Your Requests

❌ **Bad:** "Refactor the entire codebase"
✅ **Good:** "Refactor src/auth/ to use repository pattern"

Smaller scope = less context accumulation.

### 4. Reference Files Strategically

❌ **Bad:** Reference 10 files at once
✅ **Good:** Reference 2-3 most relevant files

```
# Instead of
"Review @src/auth.ts @src/user.ts @src/session.ts @src/token.ts @src/middleware.ts"

# Do
"Review @src/auth.ts — this is the main file. Check @src/user.ts only if needed."
```

### 5. Start Fresh for New Tasks

Different task? New session:

```bash
# Finish feature work
/exit

# Start new session for bug fix
claude
```

Context from feature work pollutes bug fix context.

### 6. Use Background Tasks

Background tasks have their own context:

```
"Run test suite and summarize"
[Ctrl+B]

# Main session context unaffected
```

## Recovery Strategies

### When Context Is Polluted

**Option 1: Compact**
```
/compact
```
Summarizes and continues. Works for minor pollution.

**Option 2: Clear and Re-establish**
```
/clear
"Let's continue. Here's where we are: [brief summary]"
```
Full reset. Better for severe pollution.

**Option 3: New Session**
```
/exit
claude --resume  # Or fresh start
```
Nuclear option. Use when nothing else works.

## Measured Impact

### Session Productivity by Context Management

| Strategy | Session Duration | Productivity |
|----------|-----------------|--------------|
| No management | 10-15 min | Degrades quickly |
| /compact at 70% | 25-35 min | Sustained |
| Scoped requests | 30-45 min | High |
| Combined strategies | 45-60 min | Optimal |

### Token Savings

| Technique | Token Reduction |
|-----------|-----------------|
| Optimized CLAUDE.md | -30-40% |
| Strategic file references | -20-30% |
| /compact usage | -40-50% (after compact) |
| Scoped requests | -25-35% |

## Anti-Patterns

### ❌ Loading Entire Codebase

```
# DON'T
"Analyze @src/ @lib/ @tests/ @config/"

# DO
"Analyze @src/auth/ — focus on the login flow"
```

### ❌ Long Conversational Chains

```
# DON'T
[50 back-and-forth messages refining one feature]

# DO
[10 messages] → /compact → [continue]
```

### ❌ Ignoring Warning Signs

If Claude:
- Asks something you answered
- Repeats a rejected suggestion
- Seems "confused"

**Immediately** use `/compact` or `/clear`.

---

📰 **Related Article:** [Why Your Claude Code Sessions Die After 10 Minutes](https://medium.com/@alirezarezvani)
