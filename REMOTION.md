# Remotion — Learning Notes

> Researched via gstack browse on 2026-03-23. Source: remotion.dev

---

## What is Remotion?

Remotion lets you **create real MP4 videos using React**. Instead of editing in a timeline tool, you write code. Every frame is a React render, and video is just a function of time.

- `npx create-video@latest` to scaffold a new project
- Open source core, commercial license required for companies of 4+ people
- 40k GitHub stars, 1.4M installs/month

---

## Core Concepts

### 1. Frame = Render

A video is a series of images. Remotion gives your component a **frame number**, and you render whatever you want based on it.

```tsx
import { AbsoluteFill, useCurrentFrame } from "remotion";

export const MyComp = () => {
  const frame = useCurrentFrame(); // 0, 1, 2, 3...
  return (
    <AbsoluteFill style={{ justifyContent: "center", alignItems: "center", fontSize: 100, backgroundColor: "white" }}>
      Frame: {frame}
    </AbsoluteFill>
  );
};
```

### 2. Video Properties

Every video has 4 metadata fields:

| Property | Description |
|---|---|
| `width` | Pixels wide |
| `height` | Pixels tall |
| `durationInFrames` | Total frames |
| `fps` | Frames per second |

Access them with `useVideoConfig()`:

```tsx
const { fps, durationInFrames, width, height } = useVideoConfig();
// durationInFrames / fps = total seconds
```

### 3. Composition

A **Composition** ties a React component to video metadata. Registered in `src/Root.tsx`:

```tsx
<Composition
  id="MyVideo"
  durationInFrames={150}  // 5 seconds at 30fps
  fps={30}
  width={1920}
  height={1080}
  component={MyComp}
/>
```

You can register multiple compositions (wrap in `<></>`).

---

## Animation

### Manual (math-based)

```tsx
const opacity = Math.min(1, frame / 60); // fade in over 60 frames
```

### `interpolate()` — map frames to values

```tsx
import { interpolate } from "remotion";

const opacity = interpolate(frame, [0, 60], [0, 1], {
  extrapolateRight: "clamp", // don't exceed 1
});
```

- Arg 1: variable to map (usually `frame`)
- Arg 2: input range (frame numbers)
- Arg 3: output range (values)
- Arg 4: options (`extrapolateLeft`, `extrapolateRight` = `"clamp"` | `"extend"` | `"identity"`)

### `spring()` — physics-based animation

```tsx
import { spring, useCurrentFrame, useVideoConfig } from "remotion";

const scale = spring({ fps, frame }); // 0 → 1 with natural overshoot
```

Default bounces slightly. Customize with `config: { damping, stiffness, mass }`.

**Rule:** Always animate using `useCurrentFrame()` — not CSS transitions or `setTimeout`. Remotion renders frames non-sequentially; only frame-driven animations are deterministic.

---

## Sequencing

### `<Sequence>` — time-shift components

```tsx
<>
  <Sequence durationInFrames={30}>         {/* frames 0–29 */}
    <Intro />
  </Sequence>
  <Sequence from={30} durationInFrames={30}> {/* frames 30–59 */}
    <Clip />
  </Sequence>
  <Sequence from={60}>                     {/* frames 60–end */}
    <Outro />
  </Sequence>
</>
```

Key props:
- `from` — start frame (default: 0)
- `durationInFrames` — how long to mount (default: Infinity)
- `name` — label shown in Studio timeline
- `layout` — `"absolute-fill"` (default) or `"none"` (manual layout)
- `premountFor` — mount N frames early (default: 1 second) to avoid flicker

Children of a `<Sequence>` see `useCurrentFrame()` relative to the sequence's `from`, not the global frame.

Cascading: nested sequences add their `from` values together.

### `<Series>` — play sequences back to back

Helper component that auto-calculates offsets so clips play sequentially.

---

## Parameterized Videos

Pass dynamic data to your video:

1. **Default props** — defined on `<Composition defaultProps={...}>`, used in Studio
2. **Input props** — passed at render time, override defaults
3. **`calculateMetadata()`** — async post-processing (e.g. fetch data, compute duration dynamically)
4. **Final props** → fed to your React component

Schema validation via Zod is supported (`@remotion/zod-types`).

---

## Rendering Options

| Method | When to use |
|---|---|
| Remotion Studio UI | Quick local renders via the "Render" button |
| CLI (`npx remotion render`) | Scripted/CI renders |
| SSR API (`@remotion/renderer`) | Server-side in Node.js apps |
| **AWS Lambda** | Fastest, most scalable, pay-per-render |
| Google Cloud Run | Alpha, similar to Lambda |
| GitHub Actions | CI/CD pipeline renders |

Output variants: MP4, audio-only, image sequence, still image, GIF, transparent video.

---

## Remotion Lambda (AWS)

Splits the video into chunks, renders them in parallel across many Lambda functions, then stitches them together.

- Best for: videos < 80 min at Full HD, within AWS concurrency limits
- Architecture: Lambda function + S3 bucket + Chromium layer
- Cost: very low — pay only while rendering
- Supported regions: all major AWS regions (US, EU, AP, etc.)
- Limit: 1000 concurrent Lambdas per region (can request increase)
- Max output: ~5GB / ~2 hours Full HD

---

## Remotion Player

Embed a Remotion composition in any React app without rendering to a file:

```tsx
import { Player } from "@remotion/player";
import { MyComp } from "./MyComp";

<Player
  component={MyComp}
  durationInFrames={150}
  fps={30}
  compositionWidth={1920}
  compositionHeight={1080}
  inputProps={{ name: "World" }}
/>
```

Use cases: live previews, interactive video builders, personalized video experiences that update in real-time without re-rendering.

---

## Key Packages

| Package | Purpose |
|---|---|
| `remotion` | Core — hooks, components, interpolate, spring |
| `@remotion/renderer` | Server-side rendering API |
| `@remotion/lambda` | AWS Lambda rendering |
| `@remotion/player` | Embed in React apps |
| `@remotion/captions` | Animated captions / subtitles |
| `@remotion/three` | React Three Fiber + Remotion |
| `@remotion/lottie` | Lottie animations in videos |
| `@remotion/gif` | Render as GIF |
| `@remotion/shapes` | SVG shape primitives |
| `@remotion/noise` | Perlin noise for organic motion |
| `@remotion/transitions` | Scene transition effects |
| `@remotion/google-fonts` | Google Fonts in renders |
| `@remotion/media-utils` | Audio/video analysis utilities |
| `@remotion/motion-blur` | Motion blur effect |
| `@remotion/skia` | React Native Skia graphics |
| `@remotion/zod-types` | Zod schema for props validation |

---

## Use Cases (from Showcase)

- Music visualizers
- Automated captions / subtitles
- Screencasts
- "Year in Review" personalized videos
- Social media content automation
- Video editors built on web tech (Editor Starter template)
- Data-driven video reports

---

## Remotion Studio

Local dev environment: `npm run dev`

- Visual timeline with `<Sequence>` tracks labeled by `name` prop
- Props editor (when schema defined)
- Render button with encoding settings
- Can be deployed to a cloud server for non-technical team members

---

## Quick Start

```bash
npx create-video@latest
cd my-video
npm run dev           # open Studio at localhost:3000
npx remotion render   # render to file
```

---

## Pricing

- **Free** — individuals / teams ≤ 3, unlimited local use
- **Company** — 4+ people, $250/mo minimum (+ Mux credits)
- **Creators** — $25/seat/mo (personal video creation)
- **Automators** — $0.01/render, $100/mo minimum (automated pipelines)
- **Enterprise** — custom, starting $500/mo
