# Lesson 04: Built-in slash commands

Inside a session, messages that start with `/` are commands for Claude Code itself rather than prompts for the model. These are the ones you will use daily.

## Getting help

```text
/help
```

Lists all available commands, including any custom ones you add later.

## Managing the conversation

```text
/clear
```

Wipes the conversation history and starts fresh. Use it between unrelated tasks. A long, cluttered history makes responses slower and worse.

```text
/compact
```

Summarizes the conversation so far and continues with the summary instead of the full history. Use it when you are mid-task but the session is getting long. You can steer it: `/compact keep the details about the auth refactor`.

```text
/rewind
```

Opens the checkpoint list. Claude Code snapshots your files before each change, so you can restore the code, the conversation, or both to an earlier point. This is your undo button.

## Project and account commands

```text
/init
```

Scans your project and generates a CLAUDE.md memory file (lesson 06). Run it once in every repository you work on.

```text
/model
```

Shows and switches the active model. Opus is the most capable, Sonnet is the balanced default, Haiku is fastest and cheapest.

```text
/usage
```

Shows your current usage against subscription limits. API users can use `/cost` to see spend for the session.

```text
/login
```

Switches accounts, for example between a personal and a work account.

## Configuration commands

These open interactive menus for features covered in later lessons:

- `/permissions` - view and edit permission rules (lesson 05)
- `/memory` - edit memory files (lesson 06)
- `/agents` - manage subagents (lesson 11)
- `/hooks` - configure hooks (lesson 09)
- `/mcp` - manage MCP servers (lesson 10)
- `/plugin` - browse and install plugins (lesson 12)
- `/config` - general settings menu

## Quick input shortcuts

Two prefixes work alongside slash commands:

- `!` runs a shell command directly and adds the output to the conversation, for example `!git status`
- `@` references a file so its contents are pulled into context, for example `explain @src/auth.ts`

Next: [Permission modes and settings](05-permission-modes-and-settings.md)
