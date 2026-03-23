# Design Skills for Claude Code

> Skills are add-ons that teach Claude Code new rules and behaviors. Design skills specifically improve the visual quality of what Claude builds.

---

## What Is a Skill?

A skill is a Markdown file full of instructions Claude reads before working. When a design skill is active, Claude follows its rules — like "never use Inter font" or "commit to a visual direction before writing any code."

---

## The Must-Have: `frontend-design`

**Made by: Anthropic (official)**
**Downloads: 277,000+** — the most popular design skill

This is the foundational design skill. It:
- **Bans overused fonts**: Inter, Roboto, Arial, Space Grotesk
- Forces Claude to **pick a visual style** before writing a single line of code
- Governs typography pairings, color systems, spacing, motion, and backgrounds

**How to install:**
```bash
npx skills add anthropics/claude-code --skill frontend-design
```

Once installed, every time you ask Claude to build a UI, it will first commit to a design direction (like "brutalist", "retro-futuristic", or "editorial") and then build accordingly.

---

## Other Design Skills Worth Knowing

### `impeccable` — Fine-grained design control
**Made by: pbakaus (community)**

Adds 20 specific design commands, for example:
- `/typeset` — fix typography issues
- `/arrange` — fix layout and spacing
- `/overdrive` — add extraordinary visual effects (experimental)

Also creates a `.impeccable.md` file in your project to remember your design style across sessions. Run `/teach-impeccable` once to set it up.

```bash
npx skills add pbakaus/impeccable
```

---

### `shadcn-ui` — For React / Tailwind projects
**Made by: shadcn/ui (community)**

If you're building with React and shadcn/ui components, this skill:
- Reads your project config (`components.json`)
- Knows which components you've installed
- Generates correct code on the first try (no hallucinated component names)

```bash
npx skills add shadcn-ui
```

---

### Marie Claire Dean's 63 Design Skills
**Made by: Marie Claire Dean (community, free)**

A huge collection of 63 skills covering the full design process, split into 8 groups:

| Group | What it covers |
|-------|---------------|
| Research | User research, competitive analysis |
| Systems | Design systems, tokens, consistency |
| Strategy | UX strategy, vision, metrics |
| UI | Visual design, components |
| Interaction Design | Animations, states, flows |
| Prototyping & Testing | Wireframes, user testing |
| Design Ops | Handoffs, documentation, QA |
| Everyday Toolkit | Quick utilities |

Useful commands from this collection:
- `/discover` — runs a full research discovery cycle
- `/strategize` — builds a UX strategy
- `/handoff` — generates a developer handoff with measurements, behaviors, and a QA checklist

---

### `stitch-skills` — From Google Labs
**Made by: Google Labs**

- `design-md`: Turns vague UI ideas into detailed, structured design prompts
- `enhance-prompt`: Injects design vocabulary and structure into your prompts; reads a `DESIGN.md` file for context
- `stitch-loop`: Generates complete multi-page websites iteratively

---

## Skills Already Installed on This Machine

| Skill | What it does |
|-------|-------------|
| `frontend-slides` | Creates animation-rich HTML presentations from scratch or from `.pptx` files. Use `/frontend-slides` |

---

## Where to Find More Skills

- [awesome-claude-code](https://github.com/hesreallyhim/awesome-claude-code) — Curated list of community skills
- [awesome-claude-skills](https://github.com/travisvn/awesome-claude-skills) — Community-maintained collection
- [Official Skills Docs](https://code.claude.com/docs/en/skills) — How skills work
