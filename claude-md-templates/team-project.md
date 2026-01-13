# Team Project CLAUDE.md Template

Configuration for collaborative development with code ownership and review processes.

## When to Use

- Team projects (2-10 developers)
- Startups with shared codebases
- Agency projects with multiple contributors
- Any project with PR review requirements

## Template

```markdown
# Project: [Project Name]

## Overview
[Brief description — what does this project do and who uses it?]

## Team Context
- **Team size:** [X developers]
- **Code owners:** See CODEOWNERS file
- **Review required:** All PRs need 1 approval

## Tech Stack
- **Language:** [TypeScript/Python/etc.]
- **Framework:** [Next.js/Django/etc.]
- **Database:** [PostgreSQL/etc.]
- **Infrastructure:** [AWS/GCP/etc.]
- **CI/CD:** [GitHub Actions/etc.]

## Commands
\`\`\`bash
# Development
npm run dev              # Start dev server
npm run build            # Production build

# Testing
npm test                 # Unit tests
npm run test:e2e         # E2E tests (Playwright)
npm run test:coverage    # Coverage report

# Code Quality
npm run lint             # ESLint
npm run lint:fix         # Auto-fix lint issues
npm run typecheck        # TypeScript check
npm run format           # Prettier format

# Database
npm run db:migrate       # Run migrations
npm run db:seed          # Seed dev data
\`\`\`

## Code Patterns

### File Naming
- Source files: kebab-case (`user-service.ts`)
- Components: PascalCase (`UserProfile.tsx`)
- Tests: `*.test.ts` or `*.spec.ts`
- Types: `*.types.ts`

### Component Structure
\`\`\`typescript
// Preferred component structure
export function ComponentName({ prop1, prop2 }: Props) {
  // 1. Hooks
  // 2. Derived state
  // 3. Handlers
  // 4. Effects
  // 5. Render
}
\`\`\`

### API Patterns
- REST endpoints in `/api/v1/`
- Use DTOs for request/response
- Always validate inputs with Zod
- Return consistent error format

### Error Handling
\`\`\`typescript
// Use Result pattern for expected errors
type Result<T, E> = { ok: true; value: T } | { ok: false; error: E };

// Throw only for unexpected errors
// Always include context in error messages
\`\`\`

## Git Workflow

### Branch Naming
- Features: `feature/ABC-123-short-description`
- Bugs: `fix/ABC-123-short-description`
- Hotfixes: `hotfix/ABC-123-short-description`

### Commit Messages
\`\`\`
type(scope): subject

feat(auth): add OAuth2 support
fix(api): handle null response from external service
docs(readme): update setup instructions
\`\`\`

### PR Requirements
- All tests must pass
- No lint errors
- Type check passes
- At least 1 approval
- Squash merge to main

## Constraints

### NEVER
- Push directly to main
- Skip tests for "small changes"
- Use `any` type without comment explaining why
- Commit secrets or credentials
- Delete migrations

### ALWAYS
- Create feature branch from latest main
- Write tests for new features
- Update types when changing APIs
- Run `npm run lint:fix` before committing
- Add JSDoc for public functions

### ASK FIRST
- Before changing shared utilities
- Before modifying database schema
- Before updating dependencies
- Before refactoring across multiple files

## File Structure
\`\`\`
src/
├── app/               # Next.js app router
├── components/        # Shared components
│   ├── ui/           # Base UI components
│   └── features/     # Feature-specific components
├── lib/              # Utility functions
├── hooks/            # Custom React hooks
├── services/         # Business logic
├── types/            # TypeScript types
└── __tests__/        # Test utilities
\`\`\`

## Code Owners
\`\`\`
# See CODEOWNERS for official ownership
# General guidelines:
src/auth/       → @auth-team
src/payments/   → @payments-team
src/api/        → @backend-team
\`\`\`

## Known Issues
- [Link to any known issues or tech debt]
- [Document workarounds Claude should know about]
```

## Customization Tips

1. **Link to your actual CODEOWNERS** — Claude should respect ownership
2. **Document your real git workflow** — Branch naming, commit format
3. **List actual known issues** — Prevents Claude from stumbling on them
4. **Include PR checklist** — Claude can verify before suggesting merge

---

📰 **Related Article:** [7 CLAUDE.md Mistakes That Are Killing Your Agent's Memory](https://medium.com/@alirezarezvani)
