# Lesson 01: What is Claude Code

Claude Code is a command line tool from Anthropic that puts an AI coding agent directly in your terminal. You type a request in plain English, and the agent reads your code, plans the work, edits files, runs commands, and reports back.

## Agent, not autocomplete

Tools like inline code completion suggest the next few lines while you type. Claude Code works differently. It operates in a loop:

1. You give it a task, such as "add input validation to the signup form".
2. It explores your codebase to find the relevant files.
3. It plans the change, then edits one or more files.
4. It can run tests or commands to verify the result.
5. It shows you what it did and waits for your next instruction.

This loop is what makes it "agentic". You delegate a task and review the outcome, rather than approving one keystroke at a time.

## What Claude Code can do

- Read and explain unfamiliar codebases
- Write new features across multiple files
- Fix bugs and failing tests
- Run shell commands, such as build and test scripts
- Create commits, branches, and pull requests with git
- Search the web for documentation when needed
- Automate repeated workflows through commands, hooks, and CI

## Where it runs

Claude Code lives in the terminal, so it works with any editor. There are also official extensions for VS Code and JetBrains IDEs, a desktop app, and a web version, but the terminal is the core experience and what this course teaches. Everything you learn here transfers to the other surfaces.

## How it is priced

You need one of the following:

- A Claude Pro or Max subscription, which includes Claude Code usage
- An Anthropic API key with pay-as-you-go billing
- Enterprise access through Amazon Bedrock, Google Vertex AI, or Microsoft Foundry

For learning, a Pro subscription is the simplest starting point.

## What you will learn in this course

The lessons move from basics to advanced concepts in this order: installation, everyday usage, permissions, project memory, context management, and then the extension points that make Claude Code powerful in 2026: custom commands, hooks, MCP servers, subagents, skills, and headless automation.

Next: [Installation and setup](02-installation-and-setup.md)
