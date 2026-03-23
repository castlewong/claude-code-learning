# Design Tips for Claude Code

> Practical techniques to get beautiful results from Claude Code, even as a beginner.

---

## Tip 1: Name a Visual Style

Instead of asking for "a nice design", name a specific aesthetic direction.

| Vague (avoid) | Specific (better) |
|---------------|------------------|
| "Make it look good" | "Brutalist — bold type, raw edges, high contrast" |
| "Clean and modern" | "Like Stripe's website — precise, restrained, professional" |
| "Nice UI" | "Retro-futuristic — 80s sci-fi meets clean web typography" |
| "Pretty homepage" | "Editorial magazine style — large serif headlines, white space, structured grid" |

The more specific the direction, the more distinctive the result.

---

## Tip 2: Install `frontend-design` Before Any UI Work

This official Anthropic skill resets Claude's defaults away from the "AI slop" look. Always install it when starting a new frontend project.

```bash
npx skills add anthropics/claude-code --skill frontend-design
```

It forces Claude to commit to a visual direction before writing a single line of code.

---

## Tip 3: Create a DESIGN.md File

Put this file in your project folder. Claude reads it every session.

```markdown
# Design System

## Colors
- Background: #FAFAF8 (warm white)
- Text: #1A1A1A
- Accent: #E84040 (red)

## Typography
- Display: Fraunces (variable serif)
- Body: Instrument Sans

## Personality
Bold, confident, editorial. Inspired by independent magazines.
No gradients, no cards, no Inter font.
```

This is your design memory — so you don't have to repeat yourself every time.

---

## Tip 4: Design One Thing at a Time

Good results come from focused requests:

```
❌ "Build a homepage with a hero section, features grid, testimonials, FAQ, and footer"

✓ "Build just the hero section. Use a large serif headline, one strong background color,
   and a single call-to-action button. No images yet."
```

Once the hero looks right, move to the next section.

---

## Tip 5: Use Plan Mode for Big Projects

Before Claude writes any code, you can ask it to plan first:

```
claude --permission-mode plan
```

Or press `Shift+Tab` twice inside Claude Code. Claude will read your files and tell you its approach — without touching anything — so you can review and correct before it starts.

---

## Tip 6: Ask Claude to Focus on One Design Dimension at a Time

Instead of "improve the design", be specific about what dimension:

- "Just fix the typography — sizes, line heights, and font choices"
- "Just fix the spacing — make it more breathable"
- "Just fix the colors — everything feels too dark"
- "Add one subtle animation on page load, nothing else"

This prevents Claude from changing everything at once and losing what already works.

---

## Tip 7: Reference Real Websites

You can point Claude at real websites for inspiration:

```
"Make the hero section feel like the one on linear.app —
minimal, very precise, dark background, one clear headline"
```

Claude has seen most popular websites and can draw from them.

---

## Tip 8: The "One Great Detail" Rule

> One well-orchestrated page-load animation with staggered reveals creates more impact than twenty scattered micro-interactions.

Less is more with design effects. Ask Claude for *one* great visual moment rather than many small ones.

---

## Common Mistakes to Avoid

| Mistake | Why it's a problem |
|---------|-------------------|
| Asking for "clean and minimal" | This is what Claude defaults to anyway — gives you nothing new |
| Accepting the first result | Always iterate — "make the headline bigger", "reduce the padding" |
| Changing everything at once | You lose track of what worked |
| No design reference | Claude needs direction — give it a style, mood, or example |
| Skipping DESIGN.md | Without it, Claude forgets your style between sessions |
