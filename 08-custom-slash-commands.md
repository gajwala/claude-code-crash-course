# Lesson 08: Custom slash commands

If you type the same prompt more than twice, turn it into a command. Custom slash commands are markdown files containing prompt templates, invoked by name.

## Your first command

Create a file at `.claude/commands/review.md` in your project:

```markdown
Review the current git diff for:
- bugs and edge cases
- security issues
- missing tests
Report findings as a prioritized list. Do not make any edits.
```

Now in a session:

```text
/review
```

Claude runs the file contents as a prompt. The command name comes from the filename.

## Passing arguments

Use `$ARGUMENTS` as a placeholder for everything typed after the command name. Create `.claude/commands/fix-issue.md`:

```markdown
Find GitHub issue #$ARGUMENTS using the gh CLI.
Understand the problem, locate the relevant code, and fix it.
Write a test that reproduces the bug and confirm it passes.
```

Then:

```text
/fix-issue 42
```

For multiple positional arguments, use `$1`, `$2`, and so on.

## Frontmatter options

Commands support YAML frontmatter for metadata and behavior:

```markdown
---
description: Summarize recent changes
allowed-tools: Bash(git log:*), Bash(git diff:*)
---

## Context
- Recent commits: !`git log --oneline -10`
- Current diff: !`git diff HEAD`

## Task
Summarize what changed and why it matters.
```

Two features shown here:

- `allowed-tools` grants specific permissions just for this command
- Lines with `` !`command` `` execute the shell command first and inline its output into the prompt

You can also reference files with `@path/to/file` inside a command.

## Project commands vs personal commands

- `.claude/commands/` - project scope, committed to git, shared with your team, listed as "(project)" in `/help`
- `~/.claude/commands/` - user scope, available in every project on your machine

Team conventions belong in the project. Personal habits, such as your preferred commit message style, belong in your user folder.

## Ideas worth stealing

- `/changelog` - update CHANGELOG.md from recent commits
- `/pr` - push the branch and open a pull request with a proper description
- `/onboard` - explain this codebase to a new developer
- `/security-review` - audit the diff against the OWASP Top 10

Next: [Hooks](09-hooks.md)
