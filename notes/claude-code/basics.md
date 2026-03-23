# Claude Code — Basics

> Claude Code is a command-line tool made by Anthropic that lets you talk to Claude (an AI) to help you write and edit code.

---

## What Is Claude Code?

- It runs in your **terminal** (the black window where you type commands)
- You talk to it in plain English: "add a button to my webpage"
- It reads your files, writes code, runs commands — all with your permission
- Official docs: [docs.anthropic.com/claude-code](https://docs.anthropic.com/en/docs/claude-code)

---

## How to Start

```bash
# Install (requires Node.js)
npm install -g @anthropic-ai/claude-code

# Open a project folder in terminal, then run:
claude
```

---

## Key Things Claude Code Can Do

| What | How to ask |
|------|-----------|
| Explain code | "What does this function do?" |
| Write new code | "Create a Python script that renames files" |
| Fix a bug | "This is broken, fix it: [paste error]" |
| Edit a file | "Change the button color to blue" |
| Run commands | "Run the tests" |
| Search code | "Find where the login function is" |

---

## Important Concepts

### Permissions
Claude Code always asks before doing anything risky (deleting files, running commands). You can approve or deny.

### CLAUDE.md
A file you put in your project folder to give Claude Code instructions about how to work on that project. Like a rulebook for Claude.

### Slash Commands
Type `/` to see special commands:
- `/help` — show all commands
- `/clear` — clear the conversation
- `/compact` — compress history to save space

### Context
Claude Code reads your files to understand your project. The more files it can read, the smarter its suggestions.

---

## Tips for Beginners

1. **Be specific** — "add a red button that says Submit" is better than "add a button"
2. **One thing at a time** — don't ask for 5 changes at once
3. **Read what it writes** — don't just accept, understand what changed
4. **Ask it to explain** — "explain what you just did" always works

---

## Common Terminal Commands (used with Claude Code)

```bash
cd folder-name     # go into a folder
ls                 # list files in current folder
pwd                # show where you are
```
