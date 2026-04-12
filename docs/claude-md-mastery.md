# CLAUDE.md Mastery

Most guides treat CLAUDE.md as project onboarding: list the stack, drop in the commands, maybe sketch the folder layout. That framing misses what the file actually does.

CLAUDE.md is a control file that governs Claude's behavior. It defines how the model runs, how work gets delegated, and how quality is enforced. Project specifics belong in skills. They load on demand and step back out when the job is done.

## Onboarding vs. Orchestration

The onboarding approach stuffs everything into one file: tech stack, API conventions, React patterns, deployment steps. Several things break.

**Priority saturation.** Everything in CLAUDE.md rides at high priority in the context window. When every line competes for the same top slot, nothing stands out. Your React notes collide with your API rules while you're working on a database migration.

**Context waste.** A file full of React patterns still loads on sessions where the work is a deployment script or a schema change.

**No behavioral control.** Listing the tech stack says nothing about how Claude should approach problems, delegate work, or pace multi-step jobs.

The better approach: use CLAUDE.md for orchestration. Define workflows, routing logic, quality standards, and coordination patterns. Push domain knowledge into skills.

## What Belongs in CLAUDE.md

### Core Principles

```markdown
## Core Principles

### Skills-First Workflow
Request -> Load Skills -> Gather Context -> Execute

### Context Strategy
- Delegate file explorations to sub-agents
- Reserve main context for coordination and decisions
- Skip heavy orchestration for simple, bounded tasks
```

### Routing Logic

```markdown
### Routing

Direct Execution:
- Simple tasks with clear scope
- Single-file changes
- Quick fixes

Sub-Agent Delegation:
- Multi-phase implementations
- Tasks needing specialized domain expertise
- Work that benefits from isolated context
```

### Quality Standards

```markdown
### Quality Checks
Before finalizing code:
- All inputs have validation
- Auth/authz checks exist
- External calls have error handling
- Import paths verified against codebase
```

## The Rules Directory

The `.claude/rules/` directory lets you split high-priority instructions across files with narrow scope. Each rule file rides at the same priority as CLAUDE.md, but you can target it with a path pattern:

```markdown
---
paths: src/api/**/*.ts
---

# API Rules
- Validate all input with Zod
- Return consistent error shapes
```

That rule only fires when Claude touches an API file. Your frontend work stays clean.

## The Priority Hierarchy

| Layer | Priority | Loads |
|-------|----------|-------|
| CLAUDE.md | High | Always |
| Rules Directory | High | Filtered by path pattern |
| Skills | Medium | On demand |
| File contents | Standard | When read |

## @import Syntax

Pull in external files without copying them:

```markdown
# CLAUDE.md
@docs/coding-standards.md
@docs/git-instructions.md
```

Relative paths resolve from the importing file. Recursive imports work up to 5 levels deep. Imports inside code blocks are ignored.

## CLAUDE.local.md

For personal preferences that don't belong in version control. This file loads at the same priority as CLAUDE.md but is automatically added to `.gitignore`.

Good fits: local dev URLs, personal test data, branch naming preferences, editor configurations.

## How Long Should It Be?

The popular advice to keep CLAUDE.md under 60 lines is wrong. Anthropic recommends skill files stay under 500 lines. If an on-demand skill can use 500 lines, an always-loaded control file can handle 200 to 400 lines of universal operational rules.

Optimize for relevance, not brevity. 300 lines of operational logic that applies every session beats 60 lines of project trivia that matters half the time.

For a working example of this pattern in production, [Build This Now](https://www.buildthisnow.com) ships a CLAUDE.md with skills-first routing, complexity assessment, and context management built in across 18 specialist agents.
