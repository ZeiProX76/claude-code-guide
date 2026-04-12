# Skills and Slash Commands

Skills are folders of instructions that Claude finds and loads on demand. Think of them as short reference manuals that open only when the topic fits. They solve the problem of pasting the same instructions into every session.

## What Skills Do

A skill teaches Claude *how to do something*. Procedural knowledge: workflows, checklists, domain conventions. They sit between prompts (which vanish after one turn) and MCP servers (which connect to external tools).

The loading works in two stages:

**Stage 1: Metadata only (~100 tokens).** Claude sees the name and description. Just enough to know what's available.

**Stage 2: Full instructions (when needed).** The body drops in when Claude decides a skill fits your task. Typically under 5,000 tokens.

This progressive disclosure means you can carry dozens of skills without crowding context.

## Your First Skill

Create a folder at `.claude/skills/my-skill/` with a `SKILL.md` file:

```markdown
---
name: code-review
description: Reviews code for security and performance issues when user requests a review
---

# Code Review Process

1. Check for SQL injection vulnerabilities
2. Verify input validation exists
3. Confirm error handling patterns
4. Review authentication checks
5. Flag N+1 query patterns
```

That's a complete skill. Drop it in your project and the next review request pulls it in automatically.

## Skill File Structure

```
my-skill/
  SKILL.md              # Core instructions (loads when needed)
  scripts/              # Automation scripts
  references/           # Documentation Claude can read
  assets/               # Templates and files
```

## Writing Effective Skills

Three things matter:

**1. Specific trigger descriptions.** The `description` field is what Claude scans to decide if a skill fires. "When user requests code review" beats "Helps with code." Vague descriptions never trigger reliably.

**2. Stay under 5,000 words.** Push long documentation into reference files the skill can point at. The SKILL.md itself should be focused instructions.

**3. Define boundaries.** Say what the skill should NOT touch. This prevents false triggers on unrelated prompts.

## Skills vs. Everything Else

| Feature | Skills | Prompts | Projects | MCP |
|---------|--------|---------|----------|-----|
| Provides | Procedural knowledge | One-shot instructions | Background knowledge | Tool connectivity |
| Persistence | Across conversations | Single conversation | Within project | Always connected |
| Loading | On demand | Each turn | Always in project | Always available |
| Best for | Workflows, expertise | Quick requests | Reference docs | External data |

## When to Create a Skill

The rule: any instruction you paste into more than one conversation should become a skill.

Good candidates: brand guidelines, code review checklists, deployment procedures, security audit patterns, documentation templates, git commit conventions.

Not ideal for skills: one-time requests, static project context (use CLAUDE.md), external API access (use MCP).

## Pre-Built Skills

Anthropic publishes official skills at `github.com/anthropics/skills`:

- **pdf**: Extract text and tables from PDFs
- **docx**: Create and edit Word documents
- **xlsx**: Manipulate spreadsheets
- **pptx**: Generate presentations

Claude Code also ships `/simplify` and `/batch` as built-in commands for reviews and codebase-wide migrations.

## Built-In Slash Commands

| Command | What It Does |
|---------|-------------|
| `/compact` | Compress conversation to free context |
| `/clear` | Wipe session, start fresh |
| `/model` | Switch between Sonnet and Opus |
| `/memory` | View and manage memory files |
| `/context` | Token usage breakdown |
| `/remember` | Promote session patterns to permanent memory |
| `/batch` | Run a migration across many files using worktree-isolated agents |

For a production skill set covering 21 categories (React patterns, database operations, deployment, testing, and more), [Build This Now](https://www.buildthisnow.com) ships 55+ skills that coordinate across 18 specialist agents.
