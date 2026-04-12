# Git Integration and Worktrees

Claude Code drives git straight from your terminal. Describe what you need in plain English and the commit, branch, or PR happens with your conventions applied.

## Basic Git Operations

Once Claude wraps a batch of edits, commit in one line:

```
claude "commit these changes"
```

Claude reads the diff, writes a real commit message, and runs `git commit`. No plugins. No config.

What Claude handles:
- **Any git command:** add, commit, push, pull, branch, merge
- **Commit messages:** Based on the actual changes, not generic placeholders
- **Branch creation:** For features or experiments
- **PR creation:** Using the `gh` CLI if installed
- **Conflict resolution:** Reads both versions and merges intelligently

## Setting Conventions

Drop your team's git rules into CLAUDE.md:

```markdown
## Git Conventions
- Use conventional commits: feat:, fix:, docs:, refactor:
- Keep subject lines under 72 characters
- Always run tests before committing
- Create feature branches for new work
```

Every commit after this follows your rules automatically.

## Common Workflows

### Feature Branch Flow

```bash
claude "create a feature branch called auth-improvements and switch to it"

# Work on the feature...

claude "commit the auth changes with a descriptive message"
claude "push this branch and create a PR with a summary of changes"
```

### Selective Commits

```bash
claude "show me a summary of all uncommitted changes"
claude "commit only the changes in src/auth/ with message: refactor auth module"
```

### Commit Attribution

Commits carry attribution by default so your team knows which work was AI-assisted. Customize in `settings.json`:

```json
{
  "attribution": {
    "commit": "Generated with AI\n\nCo-Authored-By: Claude <noreply>",
    "pr": "AI-assisted PR"
  }
}
```

Set either key to an empty string to disable attribution.

## Worktrees: Parallel Sessions

The `--worktree` flag is what makes Claude Code a parallel development environment.

### The Problem

You're working on a feature branch and a production bug lands. Your choices: stash and lose state, fight over the same files in two terminals, or bail entirely.

### The Solution

```bash
claude --worktree bugfix-123
```

A fresh working directory lands at `.claude/worktrees/bugfix-123/` on its own branch. The first session is untouched. Nothing collides.

### Multiple Parallel Sessions

```bash
# Terminal 1: feature work
claude --worktree feature-auth

# Terminal 2: bug fix
claude --worktree bugfix-123

# Terminal 3: experimental refactor
claude --worktree experiment-new-router
```

Three sessions. Three branches. Zero conflicts.

### Subagent Isolation

This is where worktrees pay off most. Each sub-agent Claude spawns can get its own worktree:

```
"Use worktrees for your agents when doing this refactor"
```

Without isolation, parallel sub-agents editing the same file produce silent conflicts. With isolation, each agent sees the full codebase independently. Agent A can modify `src/auth.ts` one way while Agent B tries another approach. You compare both and pick the winner.

### Custom Agents with Worktrees

Pin a custom agent to always use isolation:

```markdown
---
name: refactor-agent
description: Performs isolated refactoring work
isolation: worktree
---
You are a refactoring specialist. Analyze target code,
plan the refactor, and implement changes.
```

### Cleanup

Empty worktrees auto-delete when sessions end. Worktrees with changes prompt you to keep or remove. Add `.claude/worktrees/` to your `.gitignore`.

```bash
git worktree list    # See all worktrees
git worktree prune   # Clean up stale ones
```

### When to Use Worktrees

| Scenario | Use Worktree? |
|----------|--------------|
| Quick single-file fix | No |
| Feature work while fixing a bug | Yes |
| Multi-agent parallel execution | Yes |
| Code migration across many files | Yes |
| Exploring experimental approaches | Yes |

Rule of thumb: any time you'd reach for a separate branch to dodge conflicts, reach for a worktree instead. For a build system that orchestrates multiple worktree-isolated agents across a full SaaS pipeline, see [Build This Now](https://www.buildthisnow.com).
