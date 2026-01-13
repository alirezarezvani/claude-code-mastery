# Enterprise Patterns

Team setup, compliance, and governance for Claude Code in enterprise environments.

## Contents

| File | Description |
|------|-------------|
| [Team Setup](./team-setup.md) | Configure for multi-developer teams |
| [Compliance Patterns](./compliance-patterns.md) | HIPAA, SOC 2, PCI-DSS patterns |
| [Audit Logging](./audit-logging.md) | Track all Claude Code activity |
| [Managed Settings](./managed-settings.md) | Centralized configuration |

## Quick Start for Teams

### 1. Shared CLAUDE.md

Store in repo, commit to git:
```
project/
├── CLAUDE.md           # Shared by all developers
└── .claude/
    ├── settings.json   # Shared settings
    └── commands/       # Shared commands
```

### 2. Managed Settings

For enterprise deployment, use managed settings:

```
/etc/claude-code/managed-settings.json
```

This enforces settings across all users.

### 3. MCP Allowlists

Control which MCP servers developers can use:

```json
{
  "allowedMcpServers": [
    { "serverName": "github" },
    { "serverName": "company-internal" }
  ],
  "deniedMcpServers": [
    { "serverName": "filesystem" }
  ]
}
```

## Compliance Considerations

| Standard | Key Requirements | See |
|----------|-----------------|-----|
| HIPAA | Audit logs, access controls | [compliance-patterns.md](./compliance-patterns.md) |
| SOC 2 | Change management, monitoring | [audit-logging.md](./audit-logging.md) |
| PCI-DSS | Restricted access, encryption | [compliance-patterns.md](./compliance-patterns.md) |

## Security Model

```
┌─────────────────────────────────────────────────────────┐
│                  Managed Settings                        │
│            /etc/claude-code/managed-settings.json       │
│                  (IT/Security controlled)               │
└─────────────────────────┬───────────────────────────────┘
                          │ Overrides
                          ▼
┌─────────────────────────────────────────────────────────┐
│                  Project Settings                        │
│                .claude/settings.json                    │
│                 (Team controlled)                        │
└─────────────────────────┬───────────────────────────────┘
                          │ Overrides
                          ▼
┌─────────────────────────────────────────────────────────┐
│                   User Settings                          │
│               ~/.claude/settings.json                   │
│                 (Individual)                             │
└─────────────────────────────────────────────────────────┘
```

**Denylist always takes precedence over allowlist.**

---

📰 **Related Article:** [Hooks as Enterprise Guardrails: Compliance Without Killing Productivity](https://medium.com/@alirezarezvani)
