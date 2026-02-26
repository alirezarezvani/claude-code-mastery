# Performance Optimization

Measured data and optimization strategies for Claude Code efficiency.

## Contents

| Topic | Description | Status |
|-------|-------------|--------|
| **Token Efficiency** | Reduce token usage by 30-40% | 📋 Coming Soon |
| [Context Management](./context-management.md) | Prevent session degradation | ✅ Available |
| **Model Comparison** | Opus vs Sonnet: when to use each | 📋 Coming Soon |
| **Cost Optimization** | Minimize API costs | 📋 Coming Soon |

## Key Metrics (from 200+ hours of usage)

### Session Lifespan

| Session Type | Productive Duration | Signs of Degradation |
|--------------|--------------------|--------------------|
| Simple tasks | 30-45 minutes | Rarely degrades |
| Complex refactors | 15-25 minutes | Starts repeating, loses context |
| Multi-file work | 10-20 minutes | Forgets earlier decisions |

**Optimization:** Use `/compact` when approaching 70% context usage.

### Token Efficiency by CLAUDE.md Quality

| CLAUDE.md Quality | Token Usage | Session Productivity |
|-------------------|-------------|---------------------|
| No CLAUDE.md | Baseline (100%) | Low — rediscovers patterns |
| Basic (< 50 lines) | 85% | Medium — has core context |
| Optimized (50-150 lines) | 60-70% | High — knows your patterns |
| Overloaded (> 200 lines) | 90% | Low — skims or ignores |

**Sweet spot:** 80-120 lines of high-signal content.

### Model Cost Comparison

| Task Type | Recommended Model | Cost per Task | Accuracy |
|-----------|------------------|---------------|----------|
| Code review | Sonnet | $0.02-0.05 | 95% |
| Bug fixes | Sonnet | $0.03-0.08 | 90% |
| Simple features | Sonnet | $0.05-0.15 | 92% |
| Complex refactors | Opus | $0.20-0.50 | 98% |
| Architecture decisions | Opus | $0.30-0.80 | 97% |

**Rule:** Start with Sonnet. Upgrade to Opus only after Sonnet fails twice.

### Background Task Efficiency

| Task Type | Interactive | Background (Ctrl+B) | Savings |
|-----------|-------------|-------------------|---------|
| Test suites | $0.10 | $0.08 | 20% |
| Lint/format | $0.05 | $0.04 | 20% |
| Code generation | $0.15 | $0.12 | 20% |
| Research tasks | $0.20 | $0.15 | 25% |

**Savings:** Background tasks use ~20-25% fewer tokens due to reduced interactive overhead.

## Quick Wins

### 1. Optimize CLAUDE.md (30-40% token reduction)
```markdown
# Before: Generic
## Tech Stack
We use various technologies...

# After: Specific
## Tech Stack
TypeScript 5.3, Next.js 14, Prisma 5, PostgreSQL 15
```

### 2. Use Plan Mode for Complex Tasks
```
[Ctrl+R] → Plan mode on
"Refactor auth system"
[Claude plans first, doesn't waste tokens on wrong approaches]
```

### 3. Background Non-Interactive Tasks
```
"Run full test suite and summarize failures"
[Ctrl+B] → Runs in background
[Continue working on other tasks]
```

### 4. Compact Before Context Overflow
```
/cost  → Check context usage
[If > 70%]
/compact → Summarize and continue
```

---

📰 **Related Articles:**
- [Why Your Claude Code Sessions Die After 10 Minutes](https://medium.com/@alirezarezvani)
- [Claude Opus 4.5 vs Sonnet: I Tested Both for 30 Days](https://medium.com/@alirezarezvani)
