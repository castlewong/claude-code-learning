# Remotion Practice Projects

> Build these in order. Each one teaches a new concept. Put your practice project folders in here.

---

## Project 1 — DVD Screensaver (Beginner)

**What you build:** A logo bouncing around the screen, changing color when it hits a wall.

**What you learn:** Pure math animation, no libraries needed.

```tsx
import { AbsoluteFill, useCurrentFrame, useVideoConfig } from "remotion";

export const DVDScreensaver = () => {
  const frame = useCurrentFrame();
  const { width, height } = useVideoConfig();

  const logoW = 100;
  const logoH = 60;
  const speed = 3;

  // Total distance traveled
  const dx = (frame * speed) % ((width - logoW) * 2);
  const dy = (frame * speed * 0.7) % ((height - logoH) * 2);

  // Bounce: go forward then backward
  const x = dx < width - logoW ? dx : (width - logoW) * 2 - dx;
  const y = dy < height - logoH ? dy : (height - logoH) * 2 - dy;

  // Color cycle
  const colors = ["#FF5733", "#33FF57", "#3357FF", "#F1C40F"];
  const colorIndex = Math.floor(frame / 60) % colors.length;

  return (
    <AbsoluteFill style={{ backgroundColor: "#000" }}>
      <div style={{
        position: "absolute",
        left: x,
        top: y,
        width: logoW,
        height: logoH,
        backgroundColor: colors[colorIndex],
        borderRadius: 8,
        display: "flex",
        alignItems: "center",
        justifyContent: "center",
        color: "white",
        fontWeight: "bold",
      }}>
        DVD
      </div>
    </AbsoluteFill>
  );
};
```

---

## Project 2 — Animated Text Reveal (Beginner)

**What you build:** Words appear one by one on screen, fading and rising in.

**What you learn:** `interpolate()`, stagger timing, `<Sequence>`.

```tsx
import { AbsoluteFill, useCurrentFrame, interpolate, Sequence } from "remotion";

const Word = ({ word, delay }: { word: string; delay: number }) => {
  const frame = useCurrentFrame();

  const opacity = interpolate(frame, [delay, delay + 15], [0, 1], {
    extrapolateRight: "clamp",
  });
  const y = interpolate(frame, [delay, delay + 15], [20, 0], {
    extrapolateRight: "clamp",
  });

  return (
    <span style={{
      opacity,
      transform: `translateY(${y}px)`,
      display: "inline-block",
      marginRight: 12,
      fontSize: 72,
      color: "white",
      fontFamily: "serif",
    }}>
      {word}
    </span>
  );
};

export const TextReveal = () => {
  const words = ["Hello,", "World."];

  return (
    <AbsoluteFill style={{
      backgroundColor: "#111",
      justifyContent: "center",
      alignItems: "center",
    }}>
      {words.map((word, i) => (
        <Word key={i} word={word} delay={i * 20} />
      ))}
    </AbsoluteFill>
  );
};
```

---

## Project 3 — Animated Bar Chart (Intermediate)

**What you build:** Bars grow upward from zero to their values.

**What you learn:** `spring()` animations, data-driven rendering.

```tsx
import { AbsoluteFill, useCurrentFrame, useVideoConfig, spring } from "remotion";

const data = [
  { label: "Jan", value: 40 },
  { label: "Feb", value: 75 },
  { label: "Mar", value: 55 },
  { label: "Apr", value: 90 },
];

const Bar = ({ value, label, index }: { value: number; label: string; index: number }) => {
  const frame = useCurrentFrame();
  const { fps } = useVideoConfig();

  const progress = spring({
    frame: frame - index * 5, // stagger: each bar starts 5 frames later
    fps,
    config: { damping: 200 },
  });

  const barHeight = progress * value * 3; // scale value to pixels

  return (
    <div style={{
      display: "flex",
      flexDirection: "column",
      alignItems: "center",
      justifyContent: "flex-end",
      margin: "0 20px",
    }}>
      <div style={{
        width: 60,
        height: barHeight,
        backgroundColor: "#E84040",
        borderRadius: "4px 4px 0 0",
      }} />
      <span style={{ color: "white", marginTop: 8 }}>{label}</span>
    </div>
  );
};

export const BarChart = () => (
  <AbsoluteFill style={{
    backgroundColor: "#0A0A0A",
    justifyContent: "center",
    alignItems: "flex-end",
    paddingBottom: 100,
  }}>
    {data.map((d, i) => (
      <Bar key={i} value={d.value} label={d.label} index={i} />
    ))}
  </AbsoluteFill>
);
```

---

## Project 4 — Slide Deck (Intermediate)

**What you build:** A multi-slide presentation with transitions.

**What you learn:** `<Series>`, `<TransitionSeries>`, reusable slide components.

```bash
npm install @remotion/transitions
```

```tsx
import { AbsoluteFill, useCurrentFrame, interpolate } from "remotion";
import { TransitionSeries, springTiming } from "@remotion/transitions";
import { fade } from "@remotion/transitions/fade";

const Slide = ({ title, body, bg }: { title: string; body: string; bg: string }) => {
  const frame = useCurrentFrame();
  const opacity = interpolate(frame, [0, 15], [0, 1], { extrapolateRight: "clamp" });

  return (
    <AbsoluteFill style={{ backgroundColor: bg, padding: 80, justifyContent: "center" }}>
      <div style={{ opacity }}>
        <h1 style={{ fontSize: 72, color: "white", margin: 0 }}>{title}</h1>
        <p style={{ fontSize: 36, color: "rgba(255,255,255,0.7)", marginTop: 24 }}>{body}</p>
      </div>
    </AbsoluteFill>
  );
};

const slides = [
  { title: "Hello", body: "Welcome to my talk.", bg: "#0A0A0A" },
  { title: "The Problem", body: "Videos are hard to make.", bg: "#1A0A0A" },
  { title: "The Solution", body: "Write code instead.", bg: "#0A1A0A" },
];

export const SlideDeck = () => (
  <TransitionSeries>
    {slides.map((slide, i) => (
      <>
        <TransitionSeries.Sequence key={i} durationInFrames={90}>
          <Slide {...slide} />
        </TransitionSeries.Sequence>
        {i < slides.length - 1 && (
          <TransitionSeries.Transition
            presentation={fade()}
            timing={springTiming({ config: { damping: 200 } })}
          />
        )}
      </>
    ))}
  </TransitionSeries>
);
```

---

## Project 5 — "Wrapped" Stats Video (Advanced)

**What you build:** A Spotify Wrapped-style video showing your own stats.

**What you learn:** `delayRender` / `continueRender` (fetching data), parameterized compositions.

See the full tutorial: [Prismic: Create Videos with Code Using Remotion](https://prismic.io/blog/create-videos-with-code-remotion-tutorial)

Study this repo for architecture: [github.com/remotion-dev/github-unwrapped](https://github.com/remotion-dev/github-unwrapped)

---

## Repositories to Study

| Repo | Why it's useful |
|------|----------------|
| [remotion-dev/typewriter](https://github.com/remotion-dev/typewriter) | Clean text animation pattern |
| [remotion-dev/morph-text](https://github.com/remotion-dev/morph-text) | Advanced text morphing |
| [remotion-dev/d3-example](https://github.com/remotion-dev/d3-example) | Data visualization with D3 |
| [remotion-dev/github-unwrapped](https://github.com/remotion-dev/github-unwrapped) | Full production app, great for architecture |
| [remotion-templates](https://github.com/reactvideoeditor/remotion-templates) | Copy-paste animation snippets |

---

## Tools

| Tool | What it's for |
|------|--------------|
| [Timing Editor](https://www.remotion.dev/timing-editor) | Visually tune `interpolate` and `spring` values |
| [Remotion Bits](https://remotion-bits.dev/) | Community snippets |
| [clippkit.com](https://www.clippkit.com/) | Free Remotion components |
