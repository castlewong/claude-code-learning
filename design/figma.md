# Figma + Claude Code

> Figma is the most popular tool for designing apps and websites visually. Claude Code can connect to Figma — and when it does, the two work together in a powerful loop.

---

## What Is Figma?

Figma is a design tool where you drag, draw, and arrange visual elements to design an app or website. Designers use it to plan how things should look before any code is written.

You don't need to know Figma to use Claude Code for design — but if you do use Figma, connecting them is very powerful.

---

## The Figma MCP Integration

**Announced: February 17, 2026**

Figma released an **MCP server** (a plugin that lets AI tools read your Figma files). When connected to Claude Code, Claude can:

- Read your Figma designs directly
- Understand colors, fonts, spacing, and components from your design file
- Generate code that actually matches your design (instead of guessing)

---

## The Full Workflow: Figma ↔ Claude Code

```
Design in Figma
      ↓
Claude reads your Figma design
      ↓
Claude generates matching code
      ↓
Claude captures the live result
      ↓
That result becomes an editable Figma frame
      ↓
You refine in Figma → push updates back to code
```

This is a **bidirectional loop** — changes flow both ways between design and code.

---

## How to Set It Up

**Step 1: Install Figma MCP**

In your Claude Code settings, add the Figma MCP server. Figma provides a step-by-step guide:
[Figma MCP Setup Guide](https://help.figma.com/hc/en-us/articles/32132100833559-Guide-to-the-Figma-MCP-server)

**Step 2: Open a Figma file**

Have your design open in Figma. Claude will be able to read from it.

**Step 3: Ask Claude to build it**

```
"Build this page based on my Figma design"
```

Claude will read the design context and generate code that matches your frames.

---

## Without Figma: Screenshot Method

If you don't use Figma, you can still share visual references with Claude Code:

1. Take a screenshot of a website or design you like
2. Share it with Claude: "Make it look like this screenshot"

This is less precise than Figma MCP but works for inspiration.

---

## Do You Need Figma?

No. Many people use Claude Code for design without Figma at all — they just describe what they want in words, or use reference websites for inspiration.

Figma integration is for people who already design in Figma and want code that exactly matches their designs.
