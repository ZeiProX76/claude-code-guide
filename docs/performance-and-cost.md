# Performance and Cost

Claude Code costs real money. The right model per task, basic tracking, and a few habits can cut your bill by 40-70%.

## Pricing Tiers

| Plan | Price | Limits | Best For |
|------|-------|--------|----------|
| Pro | $20/month | ~45 messages per 5-hour window | Learning, hobby projects |
| Max 5x | $100/month | ~225 messages per 5hr | Full-time development |
| Max 20x | $200/month | ~900 messages per 5hr | Heavy daily use |
| API | Pay-per-use | Sonnet: $3/$15 per M tokens. Opus: $15/$75 | Predictable high-volume |

## Model Switching

The single biggest cost lever. Switch based on task complexity:

```
/model sonnet   # Default for 80% of tasks
/model opus     # Complex architecture decisions only
```

Start every session on Sonnet. Only switch to Opus when you need deep analysis, big refactors, or architectural reasoning. Sonnet handles implementation, debugging, and routine edits just fine.

## Track Your Usage

Install ccusage to see where tokens go:

```bash
npm install -g @ryoppippi/ccusage
ccusage daily              # Today's breakdown
ccusage monthly            # Monthly aggregation
ccusage blocks --live      # Real-time billing windows
ccusage daily --breakdown  # Per-model costs
```

Filter by date range to chase a spike:

```bash
ccusage daily --since 20250101 --until 20250131
```

## Cost-Saving Patterns

### Be Specific

```bash
# Expensive (wastes tokens on clarification rounds)
claude "make this better"

# Efficient (immediate results)
claude "optimize readability in src/auth.js: extract constants, add error handling"
```

### Batch Related Tasks

```bash
claude "update error handling in auth.js, user.js, and api.js"
```

One context load covers three files instead of three separate sessions.

### Use Planning Mode

Press `Shift+Tab` twice before expensive operations. Planning first saves money on rework. Claude sketches the approach before writing code, so you catch issues early and avoid costly do-overs.

### Manage Context Aggressively

```
/compact    # Compress when context gets long
/clear      # Start fresh for unrelated tasks
```

Long conversations spend more tokens on every new message. Compact between major tasks. Clear when switching to unrelated work.

## Environment Variables

### Suppress Non-Essential Calls

```bash
export DISABLE_NON_ESSENTIAL_MODEL_CALLS=1
```

Turns off background model calls for suggestions and tips. Core workflow is unchanged. Background token use drops.

### Prompt Caching

Claude Code uses prompt caching by default to cut cost and latency. Repeated system prompts and tool definitions get cached instead of re-sent. Leave this on unless you're debugging or benchmarking.

## Expensive Habits to Break

- **Long debugging sessions.** Break them into smaller, focused requests.
- **Repeated explanations.** Save them in CLAUDE.md or auto memory once.
- **Full codebase reviews.** Target specific files instead of asking Claude to review everything.
- **Opus for simple tasks.** Sonnet handles 80% of work at a fraction of the cost.

## The 80/20 Token Rule

The same rule from context management applies to cost: 80% of your bill comes from 20% of your interactions. Find those expensive sessions with `ccusage daily --breakdown`, identify the pattern, and fix it. Usually it's one of the habits above.

For a production build system that optimizes Claude Code usage across 18 coordinated agents with built-in cost tracking, check out [Build This Now](https://www.buildthisnow.com).
