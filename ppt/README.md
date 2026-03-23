# ppt/ — Presentation Content Folder

Put your presentation content here as `.md` files.
Claude Code will read them and build a Remotion project (animated slides or video).

---

## How to Use

1. Create a `.md` file here (e.g. `my-talk.md`)
2. Write your slides using the format below
3. Tell Claude: "build a Remotion presentation from `ppt/my-talk.md`"
4. Claude scaffolds the project, you run `npm run dev` to preview

---

## File Format

```markdown
---
title: Your Presentation Title
style: dark-minimal
fps: 30
slide_duration: 150
transition: fade
---

# First Slide
What you want to say on the first slide.

---

# Second Slide
- First bullet point
- Second bullet point
- Third bullet point

---

# A Code Example
```tsx
const opacity = interpolate(frame, [0, 30], [0, 1]);
```

---

# Summary
Key takeaway goes here.
```

---

## Frontmatter Options

| Option | What it does | Choices |
|--------|-------------|---------|
| `style` | Visual look and feel | `dark-minimal`, `light-editorial`, `brutalist`, `gradient-bold` |
| `fps` | Frames per second | `24`, `30`, `60` |
| `slide_duration` | How long each slide shows | frames — 150 = 5 seconds at 30fps |
| `transition` | Animation between slides | `fade`, `slide`, `wipe`, `none` |

---

## Visual Styles

| Style | Looks like |
|-------|-----------|
| `dark-minimal` | Dark background, red accent, serif font — like a premium tech talk |
| `light-editorial` | Cream background, navy accent, magazine-like |
| `brutalist` | Black and white, bold, raw |
| `gradient-bold` | Deep blue gradient, glowing accent — dramatic |

---

## Output Options

- **Browser slides** — Opens in Remotion Studio, plays like a slideshow
- **MP4 video** — Fully rendered video file, shareable anywhere
- **Still image** — Export any single slide as a PNG

Ask Claude which output you want when you kick off the build.
