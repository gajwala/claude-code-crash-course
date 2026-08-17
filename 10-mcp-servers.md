# Lesson 10: MCP servers

Out of the box, Claude Code can touch your files, your shell, and the web. MCP is how you connect it to everything else: databases, issue trackers, browsers, cloud providers, and internal company tools.

## What MCP is

The Model Context Protocol is an open standard for exposing tools to AI agents. An MCP server is a small program that advertises capabilities, for example "query this Postgres database" or "create a Jira ticket". Once connected, those capabilities appear as tools Claude can call, subject to the same permission system as everything else.

## Adding a server

The `claude mcp add` command registers a server. A local server that runs as a process:

```bash
claude mcp add --transport stdio postgres -- npx -y @modelcontextprotocol/server-postgres "postgresql://localhost/mydb"
```

A remote server over HTTP:

```bash
claude mcp add --transport http github https://api.githubcopilot.com/mcp/
```

Some remote servers require login. Inside a session, run `/mcp` and follow the authentication flow.

## Managing servers

```bash
claude mcp list
```

Lists configured servers and their status. Inside a session, `/mcp` shows connection state and available tools, and lets you enable or disable servers.

## Scopes

Like settings, MCP servers have three scopes:

- local: just you, just this project (the default)
- project: saved to a `.mcp.json` file committed to git, shared with the team
- user: available to you in every project

Share a team database server with `--scope project`. Keep personal tools at user scope:

```bash
claude mcp add --scope project --transport http sentry https://mcp.sentry.dev/mcp
```

## What this unlocks

With the right servers connected you can say things like:

```text
look up the error in Sentry issue PROJ-123, find the cause in our code, fix it, and comment on the Jira ticket with a summary
```

Claude chains the tools together: fetches the stack trace, reads your code, edits the fix, and updates the tracker.

## Choose servers carefully

Every connected server adds tool definitions to your context, and a malicious server could feed harmful instructions to the model. Two rules:

1. Only add servers from sources you trust, and prefer official ones.
2. Connect the few servers you actually use. Disable the rest to save context.

Next: [Subagents](11-subagents.md)
