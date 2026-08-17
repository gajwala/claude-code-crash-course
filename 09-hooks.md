# Lesson 09: Hooks

Instructions in CLAUDE.md are suggestions the model usually follows. Hooks are guarantees. A hook is a shell command that Claude Code executes automatically at specific points in its lifecycle, whether the model wants to or not.

## When hooks fire

The main events:

- PreToolUse: before a tool runs. Can block the action.
- PostToolUse: after a tool succeeds. Good for formatters and linters.
- UserPromptSubmit: when you send a message, before the model sees it.
- Stop: when Claude finishes responding.
- SessionStart: when a session begins.
- Notification: when Claude needs your attention.

## Example: format every edited file

The classic first hook. Add to `.claude/settings.json`:

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "npx prettier --write \"$CLAUDE_FILE_PATHS\""
          }
        ]
      }
    ]
  }
}
```

Now every file Claude edits gets formatted immediately. No instruction needed, no chance of the model forgetting.

## Example: block dangerous commands

A PreToolUse hook receives the tool input as JSON on stdin. Exit code 2 blocks the action and sends the message back to Claude:

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "python3 .claude/hooks/check_command.py"
          }
        ]
      }
    ]
  }
}
```

And `.claude/hooks/check_command.py`:

```python
import json, sys

data = json.load(sys.stdin)
command = data.get("tool_input", {}).get("command", "")

if "drop table" in command.lower():
    print("Blocked: destructive database command", file=sys.stderr)
    sys.exit(2)

sys.exit(0)
```

## Example: notification when Claude needs you

Long tasks run while you do something else. Get pinged when input is needed:

```json
{
  "hooks": {
    "Notification": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "osascript -e 'display notification \"Claude needs input\" with title \"Claude Code\"'"
          }
        ]
      }
    ]
  }
}
```

## Configuring hooks

Use the interactive menu rather than editing JSON by hand:

```text
/hooks
```

## A word of caution

Hooks run arbitrary shell commands with your permissions, automatically. Review any hooks that come with a cloned repository before trusting them, and keep your own hooks fast, since slow hooks delay every matching action.

Next: [MCP servers](10-mcp-servers.md)
