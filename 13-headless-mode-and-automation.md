# Lesson 13: Headless mode and automation

Everything so far has been interactive. Headless mode runs Claude Code as a one-shot command with no UI, which turns it into a building block for scripts, pipelines, and CI.

## Print mode

The `-p` flag runs a single prompt and prints the result:

```bash
claude -p "list all TODO comments in this project with file and line"
```

Claude does its full agentic work, searching files and running tools, then prints the answer and exits.

## Structured output

For scripts, request JSON:

```bash
claude -p "count the functions missing docstrings" --output-format json
```

The JSON includes the result plus metadata such as cost and duration. There is also `stream-json` for line-by-line streaming.

## Permissions without a human

Headless runs cannot show permission prompts, so denied actions simply fail. Grant what the task needs explicitly:

```bash
claude -p "fix the lint errors and run the linter to verify" \
  --allowedTools "Edit" "Bash(npm run lint:*)"
```

Resist the temptation to bypass permissions entirely on your own machine. If a task truly needs unrestricted access, run it inside a container.

## Piping data in

Claude reads stdin, which makes it a smart filter:

```bash
cat build-error.log | claude -p "explain the root cause of this failure in one paragraph"
```

```bash
git diff main | claude -p "write a conventional commit message for this change"
```

## GitHub Actions

The official integration brings the same agent to your repository's issues and pull requests. Set it up from an interactive session:

```text
/install-github-app
```

After setup, anyone on the team can mention `@claude` in an issue or PR comment:

```text
@claude fix the failing integration test in this PR
```

Claude runs in a GitHub Actions runner, makes the changes, and pushes a commit or opens a PR. Common team uses:

- Automatic code review on every pull request
- Turning well-described issues into draft PRs
- Answering questions about the codebase in issue threads

## The Agent SDK

When shell commands are not enough, the Claude Agent SDK exposes the same engine as a TypeScript and Python library. You can build custom agents with programmatic control over tools, permissions, and sessions. That is beyond a crash course, but know it exists: anything Claude Code does interactively, you can automate in code.

Next: [Workflows and best practices](14-workflows-and-best-practices.md)
