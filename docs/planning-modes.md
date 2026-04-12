# Planning Modes

Planning mode flips Claude Code into read-only analysis. Claude can scan your entire project but won't touch a single file until you approve the plan.

## The Problem It Solves

You ask for a "quick fix" and twelve files come back modified with a breaking change buried in two of them. Planning mode prevents this. You see the strategy before any code runs.

Before planning mode existed, the workaround was a prompt like "don't code anything yet, just analyze the problem." That worked sometimes. The output shape swung wildly. One run gave a single line. The next gave a novel.

With planning mode, the output is structured every time: numbered options with trade-offs, a complexity read on each approach, and the file changes listed up front.

## Activation

Press `Shift+Tab` twice to enter planning mode. The interface confirms it.

Press `Shift+Tab` once more to exit. Claude then asks for explicit confirmation before running anything.

Planning mode runs fast. No file writes, no command execution. Responses come back quickly and burn fewer tokens.

## What Claude Can Do in Planning Mode

**Allowed (read-only):**
- File content analysis (Read, LS)
- Codebase searching (Glob, Grep)
- Web research (WebSearch, WebFetch)
- Task organization (TodoRead/TodoWrite)
- Full project understanding through analysis

**Blocked:**
- File editing (Edit, MultiEdit)
- File creation (Write)
- Command execution (Bash)
- Notebook modifications
- MCP tool modifications

Claude plays strategist, not builder.

## When to Use It

### Complex Refactoring

A refactor touching multiple files, an architectural shift, or a migration path you need to evaluate. Ask Claude to analyze the codebase, map dependencies, and propose approaches with complexity ratings.

Example: "I need to migrate from CommonJS to ES modules. What's the safest approach?"

### Feature Implementation

Before building a new feature into an existing system, planning shows you which files change and how the pieces connect.

### Architecture Review

"Analyze the current project structure and suggest improvements." You get a read on file organization, dependency patterns, and architectural bottlenecks.

### Security Assessment

"Audit the authentication system for vulnerabilities." Claude reviews the auth flow and flags issues without modifying anything.

### Performance Analysis

"Review database queries and suggest optimization strategies." Claude flags N+1 problems, suggests indexing, and compares approaches.

## Workflow Patterns

**Start complex sessions with planning.** Before telling Claude to "refactor the entire user system," enter planning mode first. Know the scope before you commit.

**Use for code reviews.** Planning mode reads existing code and proposes improvements. A natural fit for tech debt work.

**Research unknown tech.** Integrating a new library? Planning mode maps the integration surface before you write anything.

**Validate before executing.** Even on smaller changes, planning shows exactly what Claude intends to touch. No surprises.

## Pairing with Other Features

Planning mode stacks well with the rest of Claude Code:

- **Context management:** Planning forces upfront analysis, preserving context further into the session
- **CLAUDE.md:** Use planning to draft CLAUDE.md changes before they go in
- **Skills:** Load relevant skills during planning to inform the analysis
- **Git worktrees:** Plan in the main branch, then execute in an isolated worktree

For a system that auto-routes tasks through 5 complexity tiers (from direct execution for trivial fixes to full multi-agent orchestration for architectural work), see how [Build This Now](https://www.buildthisnow.com) structures its planning pipeline.
