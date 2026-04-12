# Memory Systems

Claude Code runs three separate memory systems. Each one solves a different problem. Understanding which to use (and how they stack) stops you from re-explaining the same decisions every session.

## The Three Layers

| Aspect | CLAUDE.md | Auto Memory | Session Memory |
|--------|-----------|-------------|----------------|
| Who writes it | You | Claude | Claude |
| Contains | Instructions and rules | Project patterns and learnings | Conversation summaries |
| Scope | Per-project or global | Per-project | Per-session |
| Loaded at startup | Full file | First 200 lines of MEMORY.md | Relevant past sessions |
| Priority | High | Background reference | Background reference |
| Shared with team | Yes (via git) | No (local) | No (local) |

The best setup runs all three together. CLAUDE.md lays down rules. Auto memory records what Claude learns. Session memory carries the thread between conversations.

## CLAUDE.md: Your Rules

This is the only memory layer you write by hand. It loads in full at startup and sits at high priority. Put anything here that should be followed every single time: coding standards, architecture decisions, required commands, team conventions.

```markdown
# CLAUDE.md
## Standards
- Use pnpm, not npm
- Write tests before implementation
- All API responses use consistent error shapes
```

Keep it focused on behavior and rules. Project knowledge that changes over time belongs in auto memory.

## Auto Memory: Claude's Notes

Auto memory is a persistent folder where Claude logs patterns, insights, and fixes as it works. It runs by default. No setup needed.

**Where it lives:** `~/.claude/projects/<project>/memory/`

**What gets recorded:**
- Build commands and test conventions
- Debugging fixes for tricky bugs
- Architecture notes (key files, module relationships)
- Your workflow preferences

`MEMORY.md` acts as a short index. As notes grow, Claude moves detail into topic files like `debugging.md` or `patterns.md`. Only the first 200 lines of MEMORY.md load at startup, so keep it concise.

### Saving Specific Notes

Tell Claude directly:

```
"remember that we use pnpm, not npm"
"save to memory that API tests require a local Redis instance"
"note that the staging environment uses port 3001"
```

### Reviewing Memory

Run `/memory` to browse and edit memory files. Or read them from the shell:

```bash
ls ~/.claude/projects/<project>/memory/
cat ~/.claude/projects/<project>/memory/MEMORY.md
```

These are plain markdown files. Edit them whenever. Delete stale entries after big refactors.

## Session Memory: Conversation Continuity

Session Memory runs in the background during every session. It extracts structured summaries of your work and saves them to disk. Next time you open the project, relevant summaries load automatically.

**Recall signal:** Look for "Recalled X memories (ctrl+o to expand)" when a session starts.

**Extraction cadence:** First snapshot after roughly 10,000 tokens. Updates every 5,000 tokens or 3 tool calls after that.

**What gets captured:** Session title, current status, key results, and a chronological work log. Compression is the point: hours of work shrink to a focused digest.

### The /remember Command

Run `/remember` to promote session patterns into permanent project memory. Claude walks through session summaries, finds recurring patterns, and drafts updates to `CLAUDE.local.md`. You approve each addition before it's written.

This bridges automatic memory and deliberate configuration. If Claude notices across three sessions that you always correct the same thing, `/remember` flags it as a candidate for a permanent rule.

## When to Reach for What

**CLAUDE.md:** Hard rules that must be followed every time. Coding standards, architecture decisions, team conventions.

**Auto Memory:** Patterns that surface during work. Debugging fixes, build quirks, quiet preferences. Let Claude pick these up naturally.

**Session Memory:** Conversation continuity. What you discussed, what you decided, what's still open.

**Rules Directory:** When CLAUDE.md outgrows one file. Split instructions into `.claude/rules/` for cleaner structure without losing priority.

## Best Practices

- Keep MEMORY.md under 200 lines. Only the first 200 load at startup.
- Don't duplicate between CLAUDE.md and auto memory. Rules go in CLAUDE.md. Evolving patterns go in auto memory.
- Review memory files periodically. They go stale after big refactors.
- Turn auto memory off in CI with `CLAUDE_CODE_DISABLE_AUTO_MEMORY=1`.
- Save critical insights explicitly. Don't rely on Claude catching everything on its own.

For a production memory architecture that coordinates across 18 specialist agents with layered context engineering, see [Build This Now](https://www.buildthisnow.com).
