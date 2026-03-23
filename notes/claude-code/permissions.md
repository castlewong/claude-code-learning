# Claude Code — Permissions

> By default, Claude Code asks your approval before doing things. You can pre-allow actions so it works without interrupting you.

---

## Where Settings Live

| File | Scope |
|------|-------|
| `~/.claude/settings.json` | **Global** — applies to ALL projects and terminals |
| `~/.claude/settings.local.json` | Global but private (not committed to git) |
| `.claude/settings.json` (inside a project) | That project only |

---

## The Three Permission Modes

Set via `"defaultMode"` in `settings.json`:

| Mode | What it does |
|------|-------------|
| `"default"` | Asks before everything |
| `"acceptEdits"` | Auto-accepts file read/write, asks before running commands |
| `"acceptAll"` | Auto-accepts everything — no prompts at all |

---

## Allow All Permissions (Global)

Edit `~/.claude/settings.json`:

```json
{
  "permissions": {
    "allow": [
      "Bash(*)"
    ],
    "defaultMode": "acceptAll"
  }
}
```

- `"Bash(*)"` — allows any terminal command
- `"defaultMode": "acceptAll"` — skips all approval prompts

This applies to **every project and every terminal tab**.

---

## Allow Specific Commands Only

Use patterns in the `allow` array:

```json
"allow": [
  "Bash(git *)",
  "Bash(npm *)",
  "Bash(gh auth:*)"
]
```

---

## The `--dangerously-skip-permissions` Flag

You can also start Claude Code with full permissions for one session:

```bash
claude --dangerously-skip-permissions
```

This is a one-time flag — does not change your settings file.

---

## Where to Find the Settings File

```bash
open ~/.claude/settings.json    # open in default app (Mac)
```

Or edit it directly in Claude Code:
```bash
claude settings
```
