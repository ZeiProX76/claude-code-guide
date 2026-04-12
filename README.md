# Claude Code Guide

[![Claude Code](https://img.shields.io/badge/Claude-Code-blue)](https://claude.com/claude-code)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

A practical, no-fluff guide to getting the most out of Claude Code. Covers project setup, context management, skills, memory systems, planning, git workflows, and performance tuning.

## Table of Contents

| Guide | What You'll Learn |
|-------|-------------------|
| [Getting Started](docs/getting-started.md) | Installation, first session, core commands |
| [CLAUDE.md Mastery](docs/claude-md-mastery.md) | Treat CLAUDE.md as an orchestration layer, not onboarding docs |
| [Context Management](docs/context-management.md) | The 80/20 rule, /compact, task chunking, context recovery |
| [Skills and Slash Commands](docs/skills-and-commands.md) | On-demand knowledge loading, writing your first skill |
| [Memory Systems](docs/memory-systems.md) | Auto memory, session memory, and how they stack |
| [Planning Modes](docs/planning-modes.md) | Read-only analysis before committing to code changes |
| [Git Integration and Worktrees](docs/git-and-worktrees.md) | Commits, branches, PRs, and parallel worktree sessions |
| [Performance and Cost](docs/performance-and-cost.md) | Model switching, token tracking, cost-saving patterns |

## Who This Is For

- Developers picking up Claude Code for the first time
- Teams standardizing their Claude Code workflow
- Anyone tired of re-explaining context to the AI every session

## Quick Start

```bash
# Install Claude Code (requires Claude Pro subscription or higher)
npm install -g @anthropic-ai/claude-code

# Start a session in your project
cd your-project
claude

# Check your current context usage
/context

# Enter planning mode before a big change
# Press Shift+Tab twice
```

## Key Concepts

**CLAUDE.md is your control file.** It defines how Claude behaves: routing logic, delegation patterns, quality standards. Project specifics belong in skills, not here.

**Context is finite.** The 200K token window fills faster than you think. Monitor it, chunk your work, and compact between tasks.

**Skills beat repetition.** Any instruction you paste into more than one session should become a skill. They load on demand and keep your context lean.

**Memory stacks in layers.** CLAUDE.md (your rules) + auto memory (Claude's notes) + session memory (conversation continuity). All three work together.

## Built with Build This Now

This guide was created using [Build This Now](https://www.buildthisnow.com), an AI-powered SaaS build system with 18 specialist agents, 55+ skills, and a full production pipeline. If you're using Claude Code to build a SaaS product, Build This Now gives you the complete framework: auth, payments, database, email, and a coordinated AI build team that ships features end-to-end.

One-time purchase. No subscriptions. From idea to SaaS in 48 hours.

[Learn more at buildthisnow.com](https://www.buildthisnow.com)

## Related Repos

| Repo | Description |
|------|-------------|
| [Claude Code Best Practices](https://github.com/ZeiProX76/claude-code-best-practices) | Battle-tested tips distilled into actionable checklists |
| [Claude Hooks Cookbook](https://github.com/ZeiProX76/claude-hooks-cookbook) | Recipes for automating Claude Code with lifecycle hooks |
| [AI Agent Patterns](https://github.com/ZeiProX76/ai-agent-patterns) | Design patterns for multi-agent orchestration |
| [SaaS Starter Playbook](https://github.com/ZeiProX76/saas-starter-playbook) | From idea to live SaaS product, step by step |

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## Additional Resources

Check out [resources.md](resources.md) for a curated list of tools, extensions, and references.

## License

MIT
