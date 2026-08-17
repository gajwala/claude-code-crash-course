# Lesson 02: Installation and setup

This lesson gets Claude Code installed, authenticated, and running in a project.

## Install with the native installer

The recommended method on macOS and Linux:

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

On Windows PowerShell:

```powershell
irm https://claude.ai/install.ps1 | iex
```

## Install with npm

If you already have Node.js 18 or newer:

```bash
npm install -g @anthropic-ai/claude-code
```

Do not use `sudo` with this command. If you get permission errors, fix your npm prefix instead.

## Verify the installation

```bash
claude --version
```

You should see a version number. Also useful:

```bash
claude doctor
```

This checks your installation health and reports common problems.

## Authenticate

Move into any project folder and start Claude Code:

```bash
cd your-project
claude
```

On first run it opens a browser window to log in. Choose one:

- Claude account: sign in with your Pro or Max subscription
- Anthropic Console: sign in with an API account for pay-as-you-go billing

Your credentials are stored locally, so you only do this once per machine.

## Run it from a project folder

Always start `claude` from the root of the project you want to work on. Claude Code treats the current directory as its workspace: it reads files from there, and its permission rules apply there. Starting it in your home folder gives it too much to look at and makes permission prompts noisier.

## Updating

Claude Code updates itself automatically by default. To update manually:

```bash
claude update
```

Next: [Your first session](03-your-first-session.md)
