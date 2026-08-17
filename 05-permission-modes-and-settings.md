# Lesson 05: Permission modes and settings

Claude Code asks before doing anything risky. This lesson explains the permission system and how to tune it so it protects you without slowing you down.

## What requires permission

By default, Claude can read files and search the project freely. It asks before it:

- Edits or creates a file
- Runs a shell command
- Fetches a URL

Each prompt offers: allow once, allow for the rest of the session, or deny with feedback.

## The four permission modes

Press Shift+Tab in a session to cycle modes:

- Default: asks on every risky action. Best while learning.
- Accept edits: file edits are approved automatically, commands still ask. Good for focused coding.
- Plan mode: Claude can only read and analyze. It produces a plan and asks approval before touching anything. Ideal for large or unfamiliar changes.
- Bypass permissions: nothing asks. Only for isolated environments such as containers.

Plan mode deserves emphasis. For any non-trivial task, starting in plan mode and reviewing the plan before execution produces much better results than letting Claude edit immediately.

## Permission rules

Instead of answering the same prompt repeatedly, define rules. Open the interactive editor:

```text
/permissions
```

Rules live in settings files as allow, ask, and deny lists:

```json
{
  "permissions": {
    "allow": [
      "Bash(npm run test:*)",
      "Bash(git diff:*)",
      "Read(~/.zshrc)"
    ],
    "deny": [
      "Bash(rm -rf:*)",
      "Read(./.env)",
      "WebFetch"
    ]
  }
}
```

This example lets Claude run tests and git diffs without asking, and blocks it from deleting recursively, reading secrets, or fetching web pages. Deny always wins over allow.

## Where settings live

Settings are JSON files merged in this order, later ones winning:

1. `~/.claude/settings.json` - your personal defaults for all projects
2. `.claude/settings.json` - project settings, committed to git and shared with the team
3. `.claude/settings.local.json` - project settings just for you, ignored by git

When Claude asks for permission and you choose "always allow", the rule is written to one of these files.

## A sensible beginner setup

1. Stay in default mode for your first few days.
2. Allow the commands you approve constantly, such as your test and lint scripts.
3. Deny reads of `.env` and any secrets files in every project.
4. Use plan mode for anything that touches more than a couple of files.

Next: [CLAUDE.md and memory](06-claude-md-and-memory.md)
