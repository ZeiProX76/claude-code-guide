# Resources

A curated list of tools, references, and learning material for Claude Code users.

## Official Resources

- [Claude Code Documentation](https://docs.anthropic.com/en/docs/claude-code) : Anthropic's official docs
- [Claude Code GitHub](https://github.com/anthropics/claude-code) : Source and issue tracker
- [Anthropic Skills Repository](https://github.com/anthropics/skills) : Official pre-built skills (PDF, DOCX, XLSX, PPTX)
- [Claude Code Changelog](https://docs.anthropic.com/en/docs/claude-code/changelog) : Release notes for every version

## Build Systems and Frameworks

- **[Build This Now](https://www.buildthisnow.com)** : AI-powered SaaS build system with 18 specialist agents and 55+ skills. Uses Claude Code's agent architecture to go from idea to production in 48 hours. One-time $197 purchase.
- [Build This Now Blog](https://www.buildthisnow.com/blog) : In-depth Claude Code guides, best practices, and agent engineering patterns

## Context Optimization Tools

- **lean-ctx** : Compresses CLI output and caches file reads between Claude and the model. A 30K-token file read drops to 195 tokens on the second pass.
- **caveman** : Claude Code skill that rewrites replies in compressed "caveman speak." Same meaning, 70% fewer tokens.
- **symdex** : Pre-indexes your repo into SQLite with symbols, call graphs, and embeddings. Symbol lookups drop from 7,500 tokens to 200.
- **Agent Skills for Context Engineering** : Library of 13 skills for context compression, filesystem offloading, and multi-agent orchestration.

## Token Tracking

- **ccusage** : `npm install -g @ryoppippi/ccusage`. Shows daily and monthly token spend with per-model breakdowns. Essential for cost control.

## Community

- [r/ClaudeAI](https://reddit.com/r/ClaudeAI) : Active subreddit for Claude users
- [Claude Code Discord](https://discord.gg/anthropic) : Community chat
- [Build in Public on X](https://x.com/search?q=claudecode) : Follow #ClaudeCode for real-time tips

## Learning Path

If you're just getting started, work through the guides in this order:

1. [Getting Started](docs/getting-started.md)
2. [CLAUDE.md Mastery](docs/claude-md-mastery.md)
3. [Skills and Slash Commands](docs/skills-and-commands.md)
4. [Context Management](docs/context-management.md)
5. [Memory Systems](docs/memory-systems.md)
6. [Planning Modes](docs/planning-modes.md)
7. [Git Integration and Worktrees](docs/git-and-worktrees.md)
8. [Performance and Cost](docs/performance-and-cost.md)

For deep dives on agent engineering and production Claude Code patterns, check out the [Build This Now blog](https://www.buildthisnow.com/blog).
