# Remotion Animation

> Two main tools: `interpolate` for precise control, `spring` for natural motion.

---

## `interpolate()` — map frames to values

Takes a frame number and maps it to any value you need (opacity, position, scale, color, etc.)

```tsx
import { interpolate, useCurrentFrame } from "remotion";

const frame = useCurrentFrame();

// Fade in: opacity goes from 0 → 1 over frames 0–30
const opacity = interpolate(frame, [0, 30], [0, 1], {
  extrapolateRight: "clamp",  // stop at 1, don't go higher
});
```

**Parameters:**
1. The variable to map (usually `frame`)
2. Input range — `[startFrame, endFrame]`
3. Output range — `[startValue, endValue]`
4. Options — `extrapolateLeft` / `extrapolateRight`: `"clamp"` (stop), `"extend"` (keep going), `"identity"` (return input)

**Always use `extrapolateRight: "clamp"`** unless you want values to go past your range.

### Common uses

```tsx
// Fade in
const opacity = interpolate(frame, [0, 20], [0, 1], { extrapolateRight: "clamp" });

// Slide up from below
const y = interpolate(frame, [0, 20], [40, 0], { extrapolateRight: "clamp" });

// Scale up
const scale = interpolate(frame, [0, 20], [0.8, 1], { extrapolateRight: "clamp" });

// Fade out (at the end of a 90-frame clip)
const opacity = interpolate(frame, [70, 90], [1, 0], { extrapolateLeft: "clamp" });
```

---

## `spring()` — physics-based motion

Produces natural, slightly bouncy animations. No need to tune easing curves.

```tsx
import { spring, useCurrentFrame, useVideoConfig } from "remotion";

const frame = useCurrentFrame();
const { fps } = useVideoConfig();

// Goes from 0 → 1 with a natural overshoot
const scale = spring({ frame, fps });
```

Apply it as a multiplier:
```tsx
style={{ transform: `scale(${scale})` }}
```

### Customize the feel

```tsx
const scale = spring({
  frame,
  fps,
  config: {
    damping: 200,   // higher = less bounce (200 = no bounce)
    stiffness: 100, // higher = faster
    mass: 1,        // higher = heavier/slower
  },
});
```

| `damping` | Feel |
|-----------|------|
| 10–20 | Very bouncy |
| 80–100 | Slight overshoot (default) |
| 200+ | No bounce, clean snap |

---

## Stagger — animate list items one by one

Each item delays its animation by a fixed number of frames.

```tsx
const bullets = ["First point", "Second point", "Third point"];

{bullets.map((text, i) => {
  const delay = i * 10; // 10 frames between each bullet
  const opacity = interpolate(
    frame,
    [delay, delay + 15],
    [0, 1],
    { extrapolateRight: "clamp" }
  );
  const y = interpolate(
    frame,
    [delay, delay + 15],
    [20, 0],
    { extrapolateRight: "clamp" }
  );

  return (
    <div key={i} style={{ opacity, transform: `translateY(${y}px)` }}>
      {text}
    </div>
  );
})}
```

---

## Transitions Between Scenes

Use `@remotion/transitions` to add transition effects between `<Sequence>` blocks.

```bash
npm install @remotion/transitions
```

```tsx
import {
  TransitionSeries,
  springTiming,
} from "@remotion/transitions";
import { fade } from "@remotion/transitions/fade";
import { slide } from "@remotion/transitions/slide";

<TransitionSeries>
  <TransitionSeries.Sequence durationInFrames={90}>
    <Scene1 />
  </TransitionSeries.Sequence>

  <TransitionSeries.Transition
    presentation={fade()}
    timing={springTiming({ config: { damping: 200 } })}
  />

  <TransitionSeries.Sequence durationInFrames={90}>
    <Scene2 />
  </TransitionSeries.Sequence>
</TransitionSeries>
```

**Available transitions:** `fade()`, `slide()`, `wipe()`, `flip()`, `clockWipe()`, `none()`

---

## Oscillation (looping motion)

Use `Math.sin()` for continuous back-and-forth motion.

```tsx
// Oscillates between -10 and +10 px — one full cycle every 60 frames (2 seconds at 30fps)
const x = Math.sin((frame / 60) * Math.PI * 2) * 10;

style={{ transform: `translateX(${x}px)` }}
```

---

## Combining Entrance + Exit

```tsx
// Fade in over frames 0–20, fade out over frames 70–90
const opacity = interpolate(
  frame,
  [0, 20, 70, 90],
  [0,  1,  1,  0],
  { extrapolateRight: "clamp" }
);
```

`interpolate` accepts multiple keyframes — just extend both arrays together.

---

## Animation Cheat Sheet

| Effect | Code |
|--------|------|
| Fade in | `interpolate(frame, [0, 20], [0, 1], { extrapolateRight: "clamp" })` |
| Slide up | `interpolate(frame, [0, 20], [40, 0], { extrapolateRight: "clamp" })` |
| Scale up | `interpolate(frame, [0, 20], [0.8, 1], { extrapolateRight: "clamp" })` |
| Spring pop | `spring({ frame, fps, config: { damping: 14 } })` |
| Bounce in | `spring({ frame, fps, config: { damping: 10, stiffness: 200 } })` |
| Smooth arrive | `spring({ frame, fps, config: { damping: 200 } })` |
| Fade in + rise | combine opacity + translateY with same frame range |
| Loop / oscillate | `Math.sin((frame / period) * Math.PI * 2) * amplitude` |

---

## Useful Tool

**[Timing Editor](https://www.remotion.dev/timing-editor)** — visual playground to tune `interpolate` and `spring` values. See the curve before writing code.
