# Lesson 07: Managing context

Context is the model's working memory: everything it can see at once, including your messages, file contents, and command output. It is finite. Managing it well is the single biggest skill difference between new and experienced Claude Code users.

## Why context matters

When the context window fills up, Claude Code compacts the conversation automatically, summarizing older messages. Summaries lose detail. A model with a cluttered context also gets distracted and makes worse decisions. Your goal: keep context filled with relevant information only.

## Watch the context gauge

The status line shows how much context remains. You can also run:

```text
/context
```

This displays a breakdown of what is consuming space: memory files, tool definitions, conversation history, and file contents.

## Point Claude at the right files

Claude finds files on its own, but searching costs time and context. When you know where the work is, say so with `@`:

```text
refactor the retry logic in @src/http/client.ts to use exponential backoff
```

Typing `@` opens fuzzy file search. Referencing a directory like `@src/http/` gives Claude its file listing.

## One task, one conversation

The most effective habit: run `/clear` between unrelated tasks. Fixing a bug, then styling a component, then writing docs in one conversation drags all the bug-fixing context into the docs task. Clear instead, and each task starts sharp.

For long tasks, use `/compact` at natural boundaries, for example after the plan is agreed or after tests pass.

## Extended thinking

For hard problems, ask Claude to think before acting by including the word "think" in your prompt:

```text
think hard about why this deadlock happens before proposing a fix
```

Stronger phrasing requests a bigger reasoning budget. Use it for architecture decisions and tricky bugs, not routine edits, since thinking consumes context and time. You can also press Tab to toggle extended thinking on and off.

## Paste rich content

You can paste more than text:

- Paste images (screenshots, design mockups, error dialogs) directly into the prompt
- Paste long error output or logs
- Give a URL and Claude fetches the page

A screenshot of a broken layout plus "make it look like this mockup" is often the fastest way to communicate UI work.

Next: [Custom slash commands](08-custom-slash-commands.md)
