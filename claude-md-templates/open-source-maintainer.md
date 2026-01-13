# Open Source Maintainer CLAUDE.md Template

Configuration for open source projects with community contributions and public visibility.

## When to Use

- Open source libraries/frameworks
- Community-driven projects
- Projects accepting external PRs
- Public repositories with contributor guidelines

## Template

```markdown
# Project: [Project Name]

## Overview
[Brief description — what problem does this solve?]

**Repository:** [GitHub URL]
**Documentation:** [Docs URL]
**License:** [MIT/Apache 2.0/etc.]

## Project Status
- **Version:** [Current version]
- **Stability:** [Alpha/Beta/Stable]
- **Maintenance:** [Active/Maintenance mode/Looking for maintainers]

## Tech Stack
- **Language:** [TypeScript/Rust/etc.]
- **Runtime:** [Node.js 18+/Python 3.10+/etc.]
- **Build:** [tsup/esbuild/etc.]
- **Test:** [Vitest/Jest/pytest]

## Commands
\`\`\`bash
# Development
npm install              # Install dependencies
npm run dev              # Development mode with watch
npm run build            # Production build

# Testing
npm test                 # Run all tests
npm run test:watch       # Watch mode
npm run test:coverage    # Coverage report

# Code Quality
npm run lint             # ESLint
npm run format           # Prettier
npm run typecheck        # TypeScript

# Release
npm run changeset        # Create changeset for release
npm run version          # Bump versions
npm run release          # Publish to npm
\`\`\`

## Contribution Guidelines

### For External Contributors
When helping with issues or PRs from contributors:

1. **Be welcoming** — Contributors may be new to OSS
2. **Explain decisions** — Help them understand project patterns
3. **Suggest improvements** — Guide, don't just reject
4. **Follow CODE_OF_CONDUCT.md**

### PR Requirements
- All tests must pass
- New features need tests
- Documentation updates for API changes
- Changeset file for notable changes
- Follows existing code style

### Commit Convention
\`\`\`
type(scope): description

feat(parser): add support for nested objects
fix(cli): handle spaces in file paths
docs(readme): add installation instructions
chore(deps): update typescript to 5.3
\`\`\`

Types: `feat`, `fix`, `docs`, `chore`, `refactor`, `test`, `perf`

## Code Patterns

### Public API Design
\`\`\`typescript
// Public API should be:
// 1. Minimal — expose only what users need
// 2. Stable — breaking changes require major version
// 3. Documented — JSDoc for all exports

/**
 * Parses the input string into an AST.
 * @param input - The string to parse
 * @param options - Parser options
 * @returns Parsed AST
 * @throws {ParseError} If input is invalid
 * @example
 * const ast = parse('input string');
 */
export function parse(input: string, options?: ParseOptions): AST {
  // Implementation
}
\`\`\`

### Error Handling
\`\`\`typescript
// Use custom error classes for better DX
export class ParseError extends Error {
  constructor(
    message: string,
    public readonly line: number,
    public readonly column: number
  ) {
    super(\`Parse error at \${line}:\${column}: \${message}\`);
    this.name = 'ParseError';
  }
}
\`\`\`

### Backwards Compatibility
- Public API changes require deprecation warnings first
- Use `@deprecated` JSDoc tag
- Maintain deprecated APIs for at least one minor version
- Document migration path in CHANGELOG

## Documentation Requirements

### README Structure
1. What is this? (one paragraph)
2. Installation
3. Quick start example
4. API reference (or link)
5. Contributing
6. License

### Code Documentation
- JSDoc for all public functions
- Include `@example` for complex APIs
- Document edge cases and limitations
- Keep inline comments minimal but meaningful

## Constraints

### NEVER
- Break public API without major version bump
- Remove deprecated APIs without migration period
- Merge PRs without tests passing
- Commit directly to main branch
- Include user-specific config in repo

### ALWAYS
- Add changeset for notable changes
- Update types when changing APIs
- Run full test suite before release
- Document breaking changes in CHANGELOG
- Credit contributors in release notes

### ASK FIRST
- Before accepting large refactors from contributors
- Before changing core architecture
- Before adding new dependencies
- Before modifying CI/CD workflow

## Issue Triage

### Labels
- `good first issue` — Simple, well-documented issues for new contributors
- `help wanted` — Issues where community help is welcome
- `bug` — Confirmed bugs
- `enhancement` — Feature requests
- `documentation` — Docs improvements
- `breaking change` — Will require major version bump

### Response Guidelines
- Acknowledge issues within 48 hours
- Ask for reproduction if unclear
- Link to related issues/discussions
- Close stale issues with explanation

## Release Process

1. Ensure all tests pass on main
2. Run `npm run changeset` for each notable change
3. Create release PR with `npm run version`
4. Review CHANGELOG updates
5. Merge release PR
6. CI automatically publishes to npm

## File Structure
\`\`\`
src/
├── index.ts           # Public API exports
├── core/              # Core functionality
├── utils/             # Internal utilities
└── types.ts           # Type definitions

tests/
├── unit/              # Unit tests
├── integration/       # Integration tests
└── fixtures/          # Test fixtures

docs/
├── api/               # API documentation
├── guides/            # Usage guides
└── examples/          # Example projects
\`\`\`

## Community Links
- **Issues:** [GitHub Issues URL]
- **Discussions:** [GitHub Discussions URL]
- **Discord:** [Discord invite if applicable]
- **Twitter:** [Project Twitter if applicable]
```

---

📰 **Related Article:** [Building Open Source with Claude Code](https://medium.com/@alirezarezvani)
