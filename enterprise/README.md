# Enterprise Patterns

Team setup, compliance, and governance for Claude Code in enterprise environments.

## Contents

| Topic | Description | Status |
|-------|-------------|--------|
| **Team Setup** | Configure for multi-developer teams | 📋 Coming Soon |
| **Compliance Patterns** | HIPAA, SOC 2, PCI-DSS patterns | 📋 Coming Soon |
| **Audit Logging** | Track all Claude Code activity | 📋 Coming Soon |
| **Managed Settings** | Centralized configuration | 📋 Coming Soon |

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

| Standard | Key Requirements | Status |
|----------|-----------------|--------|
| **HIPAA** | Audit logs, access controls | 📋 Guide Coming Soon |
| **SOC 2** | Change management, monitoring | 📋 Guide Coming Soon |
| **PCI-DSS** | Restricted access, encryption | 📋 Guide Coming Soon |

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
