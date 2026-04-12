# Getting Started with Claude Code

Claude Code is a terminal-based AI coding assistant that reads your project, runs commands, edits files, and manages git. It operates directly in your shell. No browser tab, no VS Code extension, no web IDE.

## Prerequisites

You need three things:

1. **Node.js 18+** and npm
2. **A Claude subscription**: Pro ($20/month) at minimum. Max ($100 or $200/month) for heavier use. API pay-per-use is also an option.
3. **A project**: Claude Code works best inside an existing codebase with a git repo initialized.

## Installation

```bash
npm install -g @anthropic-ai/claude-code
```

Verify it installed:

```bash
claude --version
```

## Your First Session

Navigate to your project and start Claude:

```bash
cd ~/projects/my-app
claude
```

Claude reads your project structure, loads any CLAUDE.md files, and drops you into an interactive terminal session. Try a few things:

```
# Ask about your project
"What does this project do?"

# Make a change
"Add input validation to the signup form"

# Run a command
"Run the test suite and fix any failures"
```

Claude can read files, write files, run shell commands, search your codebase, and manage git. All from plain English instructions.

## Core Commands

These slash commands work inside any Claude Code session:

| Command | What It Does |
|---------|-------------|
| `/compact` | Compress conversation history to free up context |
| `/clear` | Wipe the session and start fresh |
| `/model` | Switch between Sonnet and Opus |
| `/memory` | View and manage loaded memory files |
| `/context` | See where your tokens are going |
| `Shift+Tab` (x2) | Enter planning mode (read-only analysis) |
| `Shift+Tab` (x1) | Exit planning mode |

## Project Setup Checklist

Before your first real work session, set up these three things:

**1. Create a CLAUDE.md file** at your project root. Start with your coding conventions and key commands:

```markdown
# CLAUDE.md

## Conventions
- Use TypeScript strict mode
- Write tests before implementation
- Follow conventional commits

## Commands
- `npm run dev` starts the dev server
- `npm test` runs the test suite
```

**2. Check auto memory** by running `/memory` inside a session. It should be enabled by default. Claude will start taking notes about your project as you work.

**3. Review your plan tier.** Run `ccusage daily` (after installing with `npm install -g @ryoppippi/ccusage`) to understand your baseline token usage.

## What to Read Next

- [CLAUDE.md Mastery](claude-md-mastery.md): Structure your CLAUDE.md as an orchestration layer
- [Context Management](context-management.md): Learn the 80/20 rule and session strategies
- [Skills and Commands](skills-and-commands.md): Stop repeating instructions every session

For a complete production setup that wires Claude Code into a full SaaS build pipeline with 18 specialist agents, check out [Build This Now](https://www.buildthisnow.com).
