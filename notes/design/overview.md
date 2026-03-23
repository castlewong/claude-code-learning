# Design with Claude Code — Overview

> Claude Code can help you build beautiful UIs — but only if you know how to guide it. Left alone, it tends to produce the same boring look every time.

---

## What "Design" Means in Claude Code

There are three ways people use Claude Code for design:

| Type | What it means |
|------|--------------|
| **Visual / UI Design** | Building websites, apps, and interfaces that look good |
| **Design-to-Code** | You design in a tool like Figma, Claude turns it into real code |
| **System Design** | Planning the structure of a project before writing any code |

This topic focuses mainly on **Visual / UI Design** — making things look great.

---

## The Problem: "AI Slop"

Without guidance, Claude always picks the most common, average-looking design choices:

- Font: Inter (or Roboto)
- Colors: Purple gradient + safe neutral grays
- Layout: Card grid
- Style: "Clean and minimal"

The result is technically correct but visually forgettable — sometimes called **"AI slop"** by designers.

The good news: there are skills and techniques specifically designed to fix this.

---

## How to Get Better Design from Claude Code

### Option 1: Install a Design Skill
Skills are like rulebooks that change how Claude approaches design. See [skills.md](skills.md) for the full list.

### Option 2: Tell Claude What You Want
Instead of "make it look good", say:
- "Use a brutalist editorial style — bold serif fonts, high contrast, intentional roughness"
- "Design this like Stripe's website — precise, professional, restrained"
- "Go maximalist — loud colors, heavy type, layered elements"

### Option 3: Create a DESIGN.md File
Put a `DESIGN.md` file in your project folder to tell Claude your design rules every session:

```markdown
# Project Design System

## Colors
- Primary: #0F172A (dark navy)
- Accent: #F59E0B (amber)

## Typography
- Headings: Playfair Display (serif)
- Body: DM Sans

## Style Direction
Editorial, high contrast, inspired by magazine layouts.
```

Claude will read this file and follow your rules automatically.

---

## Key Insight

> Claude knows *how* to make things beautiful — it has learned from millions of designs. The problem is it defaults to the average. Your job is to push it away from that center.

---

## Next Steps

- [skills.md](skills.md) — Design skills you can install
- [figma.md](figma.md) — Connect Figma to Claude Code
- [tips.md](tips.md) — Best practices and prompting tips
