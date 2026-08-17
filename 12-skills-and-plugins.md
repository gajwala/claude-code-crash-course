# Lesson 12: Skills and plugins

The final two extension points. Skills teach Claude how to do specialized work, and plugins package everything from the previous lessons for one-command installation.

## Skills

A skill is a folder containing a SKILL.md file with instructions, plus any supporting files such as scripts, templates, or reference documents. Claude reads the skill when a task matches its description.

The difference from CLAUDE.md: memory files load in full at the start of every session. Skills load only their name and description up front, and the full instructions only when relevant. This is called progressive disclosure, and it means you can have dozens of skills without burning context.

## Creating a skill

Project skills live in `.claude/skills/`, personal skills in `~/.claude/skills/`. Example, `.claude/skills/release-notes/SKILL.md`:

```markdown
---
name: release-notes
description: Writes release notes from merged pull requests. Use when preparing a release or when asked to summarize changes for users.
---

# Writing release notes

1. List merged PRs since the last tag: `gh pr list --state merged`
2. Group changes into: Features, Fixes, Breaking changes.
3. Write for end users, not developers. No commit hashes.
4. Follow the format in template.md in this skill folder.
```

Now any request like "prepare release notes for v2.1" triggers the skill automatically. Supporting files in the folder, such as template.md or a Python script, are read or executed as needed.

## Skills vs commands vs subagents

- Custom slash command: you invoke it explicitly. Best for workflows you trigger yourself.
- Skill: Claude invokes it when relevant. Best for know-how that should apply automatically.
- Subagent: separate context and persona. Best for isolation and parallelism.

They compose: a slash command can trigger work that uses a skill inside a subagent.

## Plugins

A plugin bundles commands, agents, skills, hooks, and MCP servers into one installable package. Plugins come from marketplaces, which are git repositories with a catalog file.

Browse and install inside a session:

```text
/plugin
```

Or add a marketplace and install from the command line:

```text
/plugin marketplace add anthropics/claude-code
/plugin install code-review@claude-code
```

## Why plugins matter for teams

Instead of every developer copying settings, commands, and hooks between repositories, a team publishes one plugin. Everyone installs it and gets the same reviewed, versioned setup. When the plugin updates, everyone updates.

As always: plugins run hooks and connect servers, so install only from sources you trust.

Next: [Headless mode and automation](13-headless-mode-and-automation.md)
