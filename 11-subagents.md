# Lesson 11: Subagents

A subagent is a helper agent that Claude Code spawns to handle a piece of work in its own separate context window, then reports back a summary. Think of it as delegating to a specialist so the main conversation stays clean.

## Why subagents exist

Two reasons:

1. Context isolation. A subagent can read fifty files while researching, and only its final summary lands in your main conversation. The noise stays in the subagent's context, which is discarded afterward.
2. Specialization. Each subagent has its own system prompt and tool permissions, so you can build a code reviewer that cannot edit files, or a debugger that always follows your team's process.

## Using the built-in behavior

Claude Code delegates automatically when a task fits a defined subagent. You can also ask explicitly:

```text
use a subagent to investigate how authentication works in this codebase
```

## Creating a subagent

Open the interactive generator:

```text
/agents
```

Choose to create a new agent, describe what it should do, and Claude drafts the definition. Subagents are markdown files with frontmatter, stored in `.claude/agents/` for the project or `~/.claude/agents/` for all projects.

Example, `.claude/agents/code-reviewer.md`:

```markdown
---
name: code-reviewer
description: Expert code reviewer. Use proactively after any significant code change.
tools: Read, Grep, Glob, Bash
---

You are a senior code reviewer.

When invoked:
1. Run git diff to see recent changes.
2. Review for correctness, security, readability, and missing tests.
3. Report findings grouped by severity: critical, warning, suggestion.

Be specific. Cite file and line for every finding. Do not edit any files.
```

Key fields:

- `description` tells the main agent when to delegate. The phrase "use proactively" encourages automatic use.
- `tools` limits what the subagent can do. This reviewer can read and run commands but has no edit tools.

## Parallel subagents

Independent work can run in parallel:

```text
review the frontend and backend changes in parallel using two subagents
```

This speeds up broad tasks such as large refactors or multi-part investigations.

## When not to use subagents

Subagents start with no conversation history, so they must rediscover any context they need, and their results come back as summaries. For small tasks in a conversation that already has the context loaded, delegation wastes time. Reach for subagents for research-heavy work, enforcing specialist behavior, or parallelism.

Next: [Skills and plugins](12-skills-and-plugins.md)
