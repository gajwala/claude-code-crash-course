# Lesson 06: CLAUDE.md and memory

Every session starts with a blank slate. Memory files fix that: they are instructions Claude Code loads automatically at the start of every session, so you never repeat yourself.

## CLAUDE.md

A file named CLAUDE.md at the root of your project is read at the start of each session there. It typically contains:

- What the project is and how it is structured
- Build, test, and lint commands
- Code style rules and naming conventions
- Things Claude keeps getting wrong that you want to correct permanently

Generate a starting point automatically:

```text
/init
```

Then edit it by hand. A good CLAUDE.md is short and specific:

```markdown
# Project: order-service

Node.js REST API for order processing. TypeScript, Express, Postgres.

## Commands
- npm run dev: start locally
- npm test: run unit tests
- npm run lint: check style

## Conventions
- Use async/await, never raw promises with .then
- All database access goes through src/db/repositories
- Write a test for every new endpoint

## Warnings
- Do not edit files in src/generated, they are auto-generated
```

Commit CLAUDE.md to git so your whole team benefits.

## The memory hierarchy

Claude Code loads memory from several locations, all combined:

1. `~/.claude/CLAUDE.md` - your personal preferences for every project
2. `CLAUDE.md` in the project root - shared team memory
3. `CLAUDE.local.md` in the project root - your personal notes for this project, ignored by git
4. CLAUDE.md files in subdirectories - loaded when Claude works in that directory

Put "always respond concisely" in your user file, "we use tabs not spaces" in the project file, and "my local database runs on port 5433" in the local file.

## Adding memories quickly

Start any message with `#` and Claude offers to save it to a memory file:

```text
# always run npm run lint after editing TypeScript files
```

To open and edit memory files directly:

```text
/memory
```

## Keep it lean

Memory is prepended to every conversation, so every line costs context space on every request. Prune it regularly. Ten sharp rules beat a hundred vague ones. If Claude ignores an instruction, make it more specific rather than adding more text around it.

Next: [Managing context](07-managing-context.md)
