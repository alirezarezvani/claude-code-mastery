# My Claude Code Ecosystem

A comprehensive collection of Claude Code tools, skills, and utilities I've built.

## Repository Overview

| Repository | Description | Best For |
|------------|-------------|----------|
| **[claude-code-mastery](https://github.com/alirezarezvani/claude-code-mastery)** | This repo — reference guide & cheat sheets | Learning Claude Code fundamentals |
| **[claude-code-tresor](https://github.com/alirezarezvani/claude-code-tresor)** | Production-ready skills, agents, commands (v2.7.0) | Immediate productivity boost |
| **[claude-skills](https://github.com/alirezarezvani/claude-skills)** | 48 domain-specific skills across 6 categories | Role-specific capabilities |
| **[claude-code-skill-factory](https://github.com/alirezarezvani/claude-code-skill-factory)** | Toolkit for building custom Claude Skills | Creating your own skills |
| **[ClaudeForge](https://github.com/alirezarezvani/ClaudeForge)** | CLAUDE.md Generator and maintenance tool | Setting up new projects |
| **[claude-code-aso-skill](https://github.com/alirezarezvani/claude-code-aso-skill)** | AEO/ASO Automation Framework with sub-agents | App Store Optimization |

## How These Work Together

```
┌─────────────────────────────────────────────────────────────────┐
│                      claude-code-mastery                         │
│                   (Reference & Documentation)                    │
└──────────────────────────┬──────────────────────────────────────┘
                           │
       ┌───────────────────┼───────────────────┐
       ▼                   ▼                   ▼
┌──────────────────┐ ┌──────────────────┐ ┌──────────────────┐
│ claude-code-     │ │   claude-skills  │ │   ClaudeForge    │
│     tresor       │ │                  │ │                  │
│                  │ │ 48 skills:       │ │ Generate         │
│ 8 Skills         │ │ - Marketing (5)  │ │ CLAUDE.md files  │
│ 8 Agents         │ │ - Engineering(18)│ │ for any project  │
│ 4 Commands       │ │ - Product (5)    │ │                  │
│ 20+ Prompts      │ │ - C-Level (2)    │ │                  │
│                  │ │ - PM (6)         │ │                  │
└──────────────────┘ └──────────────────┘ └──────────────────┘
                           │
                           ▼
              ┌──────────────────────┐
              │ claude-code-skill-   │
              │      factory         │
              │                      │
              │ Build your own       │
              │ custom skills        │
              └──────────────────────┘
```

## Quick Start by Goal

### "I want productivity now"
```bash
git clone https://github.com/alirezarezvani/claude-code-tresor.git
cd claude-code-tresor && ./scripts/install.sh
```

### "I need domain-specific skills"
```bash
git clone https://github.com/alirezarezvani/claude-skills.git
cd claude-skills
cp -r marketing-skill/content-creator ~/.claude/skills/
```

### "I'm setting up a new project"
```bash
curl -fsSL https://raw.githubusercontent.com/alirezarezvani/ClaudeForge/main/install.sh | bash
claudeforge init my-project
```

### "I want to build custom skills"
```bash
git clone https://github.com/alirezarezvani/claude-code-skill-factory.git
```

---

## Support

- **Issues:** Open in the relevant repository
- **Articles:** [Medium @alirezarezvani](https://medium.com/@alirezarezvani)

*All repositories are MIT licensed.*
