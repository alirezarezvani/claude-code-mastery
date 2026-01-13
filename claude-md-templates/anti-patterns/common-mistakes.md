# 7 CLAUDE.md Mistakes That Are Killing Your Agent's Memory

Common mistakes developers make with CLAUDE.md and how to fix them.

## Mistake #1: The Empty CLAUDE.md

**The Problem:**
```markdown
# My Project

This is my project.
```

**Why It Fails:**
- Claude has no context about your stack
- Re-discovers patterns every session
- Makes inconsistent decisions
- Wastes tokens on exploration

**The Fix:**
```markdown
# My Project

## Overview
E-commerce API handling 10k daily orders.

## Tech Stack
- TypeScript, Node.js 20, Express
- PostgreSQL via Prisma
- Redis for caching
- Jest for testing

## Commands
npm run dev     # Start server
npm test        # Run tests
npm run build   # Production build
```

---

## Mistake #2: The Novel

**The Problem:**
```markdown
# Project Documentation

## History
This project was started in 2019 when our team decided to...
[500 lines of backstory]

## Architecture Philosophy  
We believe in clean architecture because...
[300 lines of theory]
```

**Why It Fails:**
- Consumes context window with noise
- Buries actionable information
- Claude skims or ignores long docs

**The Fix:**
Keep CLAUDE.md under 150 lines. Put detailed docs elsewhere:
```markdown
# Project

## Quick Context
E-commerce API. See /docs/architecture.md for details.

## Commands
[actual commands here]

## Constraints
[actual constraints here]
```

**Rule:** If it doesn't change Claude's behavior, it doesn't belong in CLAUDE.md.

---

## Mistake #3: Missing Constraints

**The Problem:**
```markdown
# Project

## Tech Stack
TypeScript, React, PostgreSQL

## Commands
npm run dev
npm test
```

**Why It Fails:**
- Claude doesn't know your rules
- Uses patterns that break your codebase
- Makes decisions you'll need to undo

**The Fix:**
```markdown
## Constraints

### NEVER
- Use `any` type — we enforce strict TypeScript
- Skip error handling — all async ops need try/catch
- Use ORM raw queries — always use Prisma methods
- Delete migrations — creates deployment issues

### ALWAYS
- Use Zod for input validation
- Return typed errors, don't throw
- Add JSDoc for public functions
```

---

## Mistake #4: Outdated Commands

**The Problem:**
```markdown
## Commands
npm start        # Actually broken, we use npm run dev now
npm run test     # Actually it's npm test
```

**Why It Fails:**
- Claude runs broken commands
- Wastes time debugging command issues
- Loses trust in your documentation

**The Fix:**
Test every command before adding:
```markdown
## Commands
# Verified 2026-01-13
npm run dev          # Start dev server (port 3000)
npm test             # Run Jest tests
npm run build        # Production build
npm run lint         # ESLint check
npm run typecheck    # TypeScript check
```

---

## Mistake #5: No Code Patterns

**The Problem:**
```markdown
# Project

## Tech Stack
React, TypeScript

## Commands
npm run dev
```

**Why It Fails:**
- Claude invents its own patterns
- Inconsistent with existing code
- You spend time fixing style issues

**The Fix:**
Document YOUR patterns:
```markdown
## Code Patterns

### Component Structure
\`\`\`typescript
// We use this pattern for all components
export function ComponentName({ prop1, prop2 }: Props) {
  // 1. Hooks at top
  const [state, setState] = useState();
  
  // 2. Derived state
  const computed = useMemo(() => ..., []);
  
  // 3. Handlers
  const handleClick = () => {};
  
  // 4. Render
  return <div>...</div>;
}
\`\`\`

### Error Handling
\`\`\`typescript
// We use Result pattern, not exceptions
type Result<T> = { ok: true; data: T } | { ok: false; error: Error };
\`\`\`
```

---

## Mistake #6: Generic Placeholder Text

**The Problem:**
```markdown
## File Structure
src/
├── components/    # Components go here
├── utils/         # Utilities go here
├── types/         # Types go here
```

**Why It Fails:**
- Tells Claude nothing useful
- Doesn't explain YOUR organization
- Generic enough to be useless

**The Fix:**
Be specific about YOUR structure:
```markdown
## File Structure
src/
├── components/
│   ├── ui/           # Base components (Button, Input, Modal)
│   └── features/     # Feature components (UserCard, OrderList)
├── lib/
│   ├── api/          # API client functions
│   └── hooks/        # Custom React hooks
├── services/         # Business logic (no React)
└── types/
    ├── api.ts        # API response types
    └── domain.ts     # Domain model types
```

---

## Mistake #7: No "Ask First" Section

**The Problem:**
CLAUDE.md has NEVER and ALWAYS, but no middle ground.

**Why It Fails:**
- Claude either does things or doesn't
- No guidance for gray areas
- You miss important decisions

**The Fix:**
Add an "ASK FIRST" section:
```markdown
## Constraints

### NEVER
- Delete database migrations
- Commit secrets

### ALWAYS
- Run tests before PRs
- Use existing patterns

### ASK FIRST
- Before adding new dependencies
- Before changing database schema
- Before refactoring shared utilities
- Before modifying authentication flow
```

---

## Quick Audit Checklist

Rate your CLAUDE.md:

| Check | Points |
|-------|--------|
| Has project overview (1-2 sentences) | +1 |
| Lists tech stack with versions | +1 |
| Has working, tested commands | +1 |
| Documents code patterns with examples | +2 |
| Has NEVER constraints | +2 |
| Has ALWAYS constraints | +1 |
| Has ASK FIRST section | +2 |
| Under 150 lines | +1 |
| Updated in last 30 days | +1 |

**Score:**
- 0-4: Critical — Claude is flying blind
- 5-7: Functional — Basic guidance in place
- 8-10: Optimized — Claude has full context
- 11-12: Excellent — Production-grade configuration

---

## Template: Minimum Viable CLAUDE.md

If you're starting from scratch, use this:

```markdown
# [Project Name]

## Overview
[One sentence: what is this?]

## Tech Stack
[Language, framework, database, key deps]

## Commands
\`\`\`bash
npm run dev     # [what it does]
npm test        # [what it does]
npm run build   # [what it does]
\`\`\`

## Constraints

### NEVER
- [Thing that breaks your project]
- [Thing that breaks your project]

### ALWAYS
- [Pattern you want enforced]
- [Pattern you want enforced]

### ASK FIRST
- [Decision you want to review]
- [Decision you want to review]
```

---

📰 **This content is from:** [7 CLAUDE.md Mistakes That Are Killing Your Agent's Memory](https://medium.com/@alirezarezvani)
