# Lesson 14: Workflows and best practices

You now know every major feature. This closing lesson covers how experienced users combine them into workflows that consistently produce good results.

## Explore, plan, code, verify

The single most reliable workflow for non-trivial tasks:

1. Explore. Ask Claude to read the relevant code and explain the current behavior. No edits yet.
2. Plan. Switch to plan mode (Shift+Tab twice) and ask for an implementation plan. Read it critically and push back on anything wrong. This is the highest-leverage moment: correcting a plan costs one message, correcting bad code costs many.
3. Code. Approve the plan and let Claude implement it.
4. Verify. Have Claude run tests, then review the diff yourself before committing.

Skipping straight to "code" works for small fixes. For everything else, the plan step pays for itself.

## Test-driven development works even better with agents

Give Claude a target it can verify against:

```text
write failing tests for the discount calculation rules described in the ticket. Do not implement anything yet.
```

Then:

```text
now implement the code to make those tests pass. Do not modify the tests.
```

The agent iterates against the tests until they pass. Clear success criteria transform output quality, and this applies beyond tests: mockup screenshots for UI work and expected output samples for data work serve the same purpose.

## Course corrections beat restarts

- Press Escape the moment Claude goes off track, then redirect.
- Press Escape twice to rewrite an earlier message and branch differently.
- Use `/rewind` to restore code checkpoints when a change went wrong.
- Use `/clear` when switching to an unrelated task.

Do not let a wrong approach run to completion out of politeness. It is a tool.

## Be specific

Vague prompts produce vague results. Compare:

```text
add tests for the user service
```

```text
add unit tests for UserService.create: duplicate email, invalid email format, and password below minimum length. Follow the patterns in tests/services/order.test.ts
```

The second prompt costs thirty extra seconds and saves three review cycles.

## Commit often

Ask Claude to commit after each working increment. Small commits plus checkpoints mean any mistake is cheap to undo. Claude writes good commit messages from the diff, and a `/pr` custom command makes shipping a one-liner.

## Review everything

You are responsible for what ships. Read diffs before approving, run the tests, and treat Claude's output like a pull request from a fast, talented, occasionally overconfident teammate.

## Where to go next

- Official docs: https://docs.anthropic.com/en/docs/claude-code
- Build a CLAUDE.md and two custom commands for your main project this week
- Add one hook, one MCP server, and one subagent as needs come up
- Explore the Agent SDK when you want to build automation beyond the terminal

You have completed the crash course.
