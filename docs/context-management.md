# Context Management

Claude Code's context window is active working memory, not a passive archive. Once it fills up, Claude struggles to hold your project in view. You'll see inconsistent code, repeated questions, lost decisions, and breaking changes that trample patterns set up minutes ago.

## The 80/20 Rule

Leave the last 20% of the context window alone on any serious multi-file task. Refactors, new features, and deep debugging all need working memory to track how components relate. Burn through that reserve and quality drops.

**Stop at 80% for:** large refactors, multi-file features, complex debugging, cross-file code reviews.

**Safe to continue past 80% for:** single-file edits, utility functions, documentation updates, localized bug fixes.

Check your token percentage in the status bar at the bottom of the terminal. Make it a habit before starting any new task.

## /compact: When and How

The `/compact` command squeezes your conversation into a summary. Claude keeps rolling session memory in the background, so compaction grabs the existing summary instead of re-summarizing from zero. It runs in seconds.

**When to compact:**
- After completing a major feature, before starting the next one
- Before switching from research to implementation
- When Claude starts repeating questions or contradicting earlier decisions

**When NOT to compact:**
- Mid-debugging when error messages and stack traces matter
- During complex refactoring where file-level detail is critical
- Right before integration work that depends on component context

## Task Chunking

Don't run Claude into the ground on one long session. Slice work into context-sized chunks with clean breaks.

```bash
# Session 1: Build the component
claude "Build the UserProfile component with all props and styling"

# Session 2: Integrate it
claude "Integrate UserProfile with the dashboard layout"
```

Finish research phases before implementation. Complete components before integration. Between sessions, write handoff notes:

```
claude "Create handoff notes covering:
1. Current project state
2. Patterns we established
3. Key decisions and reasoning
4. Next steps with implementation details"
```

Stash the notes in your project. Start fresh, point Claude at them, and you're back in sync.

## Context Recovery

When context is already degraded (compaction hit, session crashed, or drift got bad), run this sequence:

1. Reference your most recent checkpoint notes
2. Ask Claude to scan recent files and identify patterns
3. Provide a brief project overview focusing on current components
4. Start with small, isolated tasks while context rebuilds
5. Use `/clear` when context is too corrupted. A clean start with good handoff notes is faster than fighting degraded context.

## Monitoring Context

**Status bar.** Token percentage at the bottom of the terminal. Your main signal.

**`/context` command.** Shows where tokens are going: system prompt, tools, memory files, skills, conversation history. If memory files chew 15% before you've typed anything, trim them.

## Open-Source Tools That Help

Four tools that compound on each other:

- **symdex**: Pre-indexes your repo so Claude jumps to exact symbols instead of reading entire files. 7,500 tokens to 200.
- **lean-ctx**: Compresses CLI output and caches file reads. 30K tokens to 195 on cached reads.
- **caveman**: Rewrites replies in compressed style. Same meaning, 70% fewer tokens.
- **Agent Skills for Context Engineering**: 13 skills for session-level context management.

Install symdex first, then lean-ctx, then caveman, then the context engineering skills. Each attacks a different layer.

Combined effect: roughly 10x less context per session at zero workflow change.

For production context engineering patterns across multi-agent systems, see the guides at [Build This Now](https://www.buildthisnow.com/blog).
