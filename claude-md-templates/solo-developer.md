# Solo Developer CLAUDE.md Template

Minimal, fast configuration for personal projects and rapid iteration.

## When to Use

- Personal projects
- Side projects
- Prototypes and MVPs
- Learning/experimentation
- Solo freelance work

## Template

```markdown
# Project: [Your Project Name]

## Overview
[One sentence description of what this project does]

## Tech Stack
- Language: [TypeScript/Python/etc.]
- Framework: [Next.js/FastAPI/etc.]
- Database: [PostgreSQL/MongoDB/etc.]
- Key deps: [list 3-5 most important]

## Commands
\`\`\`bash
# Development
npm run dev          # Start dev server
npm run build        # Production build
npm test             # Run tests
npm run lint         # Lint check
npm run typecheck    # Type check
\`\`\`

## Code Patterns

### Naming
- Files: kebab-case (user-auth.ts)
- Components: PascalCase (UserAuth.tsx)
- Functions: camelCase (getUserAuth)
- Constants: SCREAMING_SNAKE (MAX_RETRIES)

### Structure
- Keep files under 200 lines
- One component per file
- Colocate tests with source files

### Error Handling
- Always use try/catch for async operations
- Return typed errors, don't throw
- Log errors with context

## Constraints

### NEVER
- Commit .env files
- Use `any` type in TypeScript
- Skip error handling
- Delete files without asking

### ALWAYS
- Run tests before suggesting PR
- Use existing patterns from codebase
- Ask before major refactors

## File Structure
\`\`\`
src/
├── components/     # React components
├── lib/           # Utility functions
├── hooks/         # Custom hooks
├── types/         # TypeScript types
└── app/           # Next.js app router
\`\`\`
```

## Customization Tips

1. **Add your actual commands** — Don't leave placeholders
2. **List real constraints** — What has bitten you before?
3. **Keep it under 100 lines** — More than that, use Team template

## Example: Next.js Project

```markdown
# Project: MyApp Dashboard

## Overview
Admin dashboard for MyApp SaaS platform.

## Tech Stack
- TypeScript, Next.js 14 (App Router)
- Tailwind CSS, shadcn/ui
- PostgreSQL via Prisma
- Auth: NextAuth.js

## Commands
\`\`\`bash
npm run dev           # localhost:3000
npm run build         # Production build
npm run db:push       # Push schema changes
npm run db:studio     # Open Prisma Studio
npm test              # Jest tests
\`\`\`

## Code Patterns
- Use server components by default
- Client components only for interactivity
- Form validation with Zod
- API routes in app/api/

## Constraints
### NEVER
- Use `use client` unnecessarily
- Skip Zod validation on inputs
- Hardcode URLs (use env vars)

### ALWAYS
- Use Prisma transactions for multi-step ops
- Add loading.tsx for async pages
```

---

📰 **Related Article:** [7 CLAUDE.md Mistakes That Are Killing Your Agent's Memory](https://medium.com/@alirezarezvani)
