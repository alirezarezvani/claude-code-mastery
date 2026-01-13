# Monorepo CLAUDE.md Template

Configuration for multi-package repositories with cross-package dependencies.

## When to Use

- Monorepos (Turborepo, Nx, Lerna)
- Multi-package npm workspaces
- Projects with shared libraries
- Microservices in single repo

## Template

```markdown
# Project: [Monorepo Name]

## Overview
[Brief description of the monorepo and its packages]

## Monorepo Structure
\`\`\`
[repo-name]/
├── apps/
│   ├── web/           # Next.js web application
│   ├── api/           # Node.js API server
│   └── mobile/        # React Native app
├── packages/
│   ├── ui/            # Shared UI components
│   ├── config/        # Shared configurations
│   ├── utils/         # Shared utilities
│   └── types/         # Shared TypeScript types
└── tooling/
    ├── eslint/        # ESLint configurations
    └── typescript/    # TypeScript configurations
\`\`\`

## Tech Stack
- **Monorepo tool:** [Turborepo/Nx/etc.]
- **Package manager:** [pnpm/npm/yarn]
- **Language:** TypeScript (strict mode)
- **Apps:** [Next.js, Express, React Native]
- **Packages:** [Shared libs description]

## Commands

### Root Level
\`\`\`bash
# Install all dependencies
pnpm install

# Build all packages
pnpm build

# Run all tests
pnpm test

# Lint entire repo
pnpm lint

# Type check entire repo
pnpm typecheck
\`\`\`

### Filtered Commands
\`\`\`bash
# Build specific package
pnpm --filter @repo/web build

# Run dev for specific app
pnpm --filter @repo/api dev

# Test specific package
pnpm --filter @repo/utils test

# Build package and its dependencies
pnpm --filter @repo/web... build
\`\`\`

### Workspace Commands
\`\`\`bash
# Add dependency to specific package
pnpm --filter @repo/web add axios

# Add shared package as dependency
pnpm --filter @repo/web add @repo/ui

# Add dev dependency to root
pnpm add -D -w typescript
\`\`\`

## Package Relationships

### Dependency Graph
\`\`\`
apps/web ──────┬──► packages/ui
               ├──► packages/utils
               └──► packages/types

apps/api ──────┬──► packages/utils
               └──► packages/types

packages/ui ───┬──► packages/utils
               └──► packages/types
\`\`\`

### Internal Package References
\`\`\`json
// apps/web/package.json
{
  "dependencies": {
    "@repo/ui": "workspace:*",
    "@repo/utils": "workspace:*",
    "@repo/types": "workspace:*"
  }
}
\`\`\`

## Code Patterns

### Cross-Package Imports
\`\`\`typescript
// ✅ CORRECT - Import from package
import { Button } from '@repo/ui';
import { formatDate } from '@repo/utils';
import type { User } from '@repo/types';

// ❌ WRONG - Relative imports across packages
import { Button } from '../../../packages/ui/src';
\`\`\`

### Shared Types
\`\`\`typescript
// packages/types/src/user.ts
export interface User {
  id: string;
  email: string;
  name: string;
}

// Use in any package
import type { User } from '@repo/types';
\`\`\`

### Shared Utilities
\`\`\`typescript
// packages/utils/src/format.ts
export function formatCurrency(amount: number): string {
  return new Intl.NumberFormat('en-US', {
    style: 'currency',
    currency: 'USD',
  }).format(amount);
}
\`\`\`

## Context for Claude

### When Working on Specific Package
Tell Claude which package you're focused on:
\`\`\`
"I'm working on apps/web. Focus changes there but check packages/ui for existing components first."
\`\`\`

### When Making Cross-Package Changes
\`\`\`
"This change affects both packages/utils and apps/api. Update the utility first, then update API usage."
\`\`\`

### Understanding Build Order
Turborepo handles build order automatically based on dependencies:
1. `packages/types` (no deps)
2. `packages/utils` (depends on types)
3. `packages/ui` (depends on types, utils)
4. `apps/*` (depends on packages)

## Constraints

### NEVER
- Import using relative paths across packages
- Duplicate code that should be in shared package
- Add app-specific code to shared packages
- Publish packages without building dependencies first
- Modify another package's internals directly

### ALWAYS
- Use workspace protocol for internal deps (`workspace:*`)
- Export from package index (`packages/ui/src/index.ts`)
- Keep shared packages generic (no app-specific logic)
- Update all consumers when changing shared package API
- Run `pnpm build` from root after shared package changes

### ASK FIRST
- Before adding new shared packages
- Before moving code between packages
- Before changing package dependencies
- Before modifying turborepo.json/nx.json

## Package Guidelines

### apps/ (Applications)
- Contain app-specific code only
- Import from packages/ for shared functionality
- Own their own routing, pages, API routes
- Can have app-specific components

### packages/ (Shared Libraries)
- Generic, reusable code only
- No app-specific business logic
- Well-documented exports
- Semantic versioning for breaking changes

### tooling/ (Configurations)
- ESLint, TypeScript, Prettier configs
- Shared across all packages
- Extend base configs, override as needed

## Troubleshooting

### Build Failures
\`\`\`bash
# Clean all build artifacts
pnpm clean

# Rebuild from scratch
pnpm build

# Build with verbose output
pnpm build --verbose
\`\`\`

### Type Errors Across Packages
\`\`\`bash
# Rebuild types package first
pnpm --filter @repo/types build

# Then rebuild dependent packages
pnpm build
\`\`\`

### Dependency Issues
\`\`\`bash
# Clear node_modules and reinstall
rm -rf node_modules **/node_modules
pnpm install
\`\`\`
```

---

📰 **Related Article:** [Managing Monorepos with Claude Code](https://medium.com/@alirezarezvani)
