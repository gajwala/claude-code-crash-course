# Lesson 03: Your first session

Time to actually use Claude Code. Open a terminal in a small project you do not mind experimenting on.

## Starting and stopping

```bash
claude
```

This opens an interactive session called the REPL. You type messages, Claude responds. To leave, type `/exit` or press Ctrl+C twice.

You can also start with an initial prompt:

```bash
claude "explain what this project does"
```

## Ask questions first

The safest way to learn is to ask read-only questions. Try these in your project:

```text
what does this project do?
```

```text
where is the entry point of this application?
```

```text
find all the places that read environment variables
```

Claude searches the codebase itself. You do not need to paste code or tell it which files to open.

## Make your first edit

Now ask for a small change:

```text
add a comment at the top of the main file explaining what it does
```

Before writing the file, Claude shows a diff and asks for permission. You can approve once, approve for the rest of the session, or reject with feedback. This permission system is covered in depth in lesson 05.

## Run a command through Claude

```text
run the tests and fix anything that fails
```

Claude asks permission to run the test command, reads the output, and edits code until the tests pass. This edit-run-fix loop is the core workflow.

## Essential keyboard controls

- Escape: interrupt Claude while it is working. Your session stays intact and you can redirect it.
- Escape twice: jump back to an earlier message and rewrite history from there.
- Up arrow: recall previous messages you typed.
- Shift+Tab: cycle permission modes (lesson 05).

Interrupting is normal. If Claude heads in the wrong direction, press Escape and clarify rather than letting it finish.

## Resume a conversation

Sessions are saved. To continue where you left off:

```bash
claude --continue
```

To pick from a list of past sessions:

```bash
claude --resume
```

Next: [Built-in slash commands](04-built-in-slash-commands.md)
