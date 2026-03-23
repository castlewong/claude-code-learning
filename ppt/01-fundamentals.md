# Remotion Fundamentals

> The core idea: a video is just a React component that knows what frame it's on. You write the component, Remotion captures every frame, then stitches them into a video.

---

## The 4 Building Blocks

### 1. `useCurrentFrame()` — the heartbeat of every animation

```tsx
import { useCurrentFrame } from "remotion";

export const MyComp = () => {
  const frame = useCurrentFrame(); // 0, 1, 2, 3...

  return <div>Frame: {frame}</div>;
};
```

Everything animates by reading this number. Frame 0 = first frame. At 30fps, frame 30 = 1 second in.

---

### 2. `useVideoConfig()` — your video's metadata

```tsx
import { useVideoConfig } from "remotion";

const { fps, durationInFrames, width, height } = useVideoConfig();

// useful calculation:
const totalSeconds = durationInFrames / fps; // e.g. 90 / 30 = 3 seconds
```

---

### 3. `<Composition>` — registers your video

Goes in `src/Root.tsx`. Tells Remotion the size, length, and which component to render.

```tsx
import { Composition } from "remotion";
import { MyComp } from "./MyComp";

export const RemotionRoot = () => (
  <Composition
    id="MyVideo"
    component={MyComp}
    durationInFrames={90}   // 3 seconds at 30fps
    fps={30}
    width={1920}
    height={1080}
  />
);
```

---

### 4. `<AbsoluteFill>` — fills the whole canvas

Every slide/scene starts with this. It's just `position: absolute; top: 0; left: 0; width: 100%; height: 100%`.

```tsx
import { AbsoluteFill } from "remotion";

export const MyComp = () => (
  <AbsoluteFill style={{ backgroundColor: "black", justifyContent: "center", alignItems: "center" }}>
    <h1 style={{ color: "white" }}>Hello</h1>
  </AbsoluteFill>
);
```

---

## The Golden Rule

> **Never** use CSS transitions, `setTimeout`, or `setInterval` for animation in Remotion.

Remotion renders frames out of order (it might render frame 60 before frame 10). Only `useCurrentFrame()` is reliable. All animation must be a pure function of the frame number.

```tsx
// ✅ Correct — pure function of frame
const opacity = frame / 30; // goes from 0 to 1 over 30 frames

// ❌ Wrong — not deterministic
setTimeout(() => setOpacity(1), 1000);
```

---

## Time Math

```
frame / fps = seconds into the video

Examples at 30fps:
  frame 0   = 0.0s
  frame 30  = 1.0s
  frame 60  = 2.0s
  frame 150 = 5.0s
```

---

## Sequencing — Show Things at Different Times

### `<Sequence>` — offset a component in time

```tsx
import { Sequence } from "remotion";

export const MyVideo = () => (
  <>
    <Sequence durationInFrames={60}>
      <Intro />          {/* plays frames 0–59 */}
    </Sequence>

    <Sequence from={60} durationInFrames={90}>
      <MainContent />    {/* plays frames 60–149 */}
    </Sequence>

    <Sequence from={150}>
      <Outro />          {/* plays from frame 150 to end */}
    </Sequence>
  </>
);
```

Inside `<Sequence>`, `useCurrentFrame()` resets to 0. So `<Intro>` always sees frames starting at 0, even though it starts later in the video.

### `<Series>` — play scenes back to back (auto-calculates offsets)

```tsx
import { Series } from "remotion";

<Series>
  <Series.Sequence durationInFrames={60}>
    <Intro />
  </Series.Sequence>
  <Series.Sequence durationInFrames={90}>
    <MainContent />
  </Series.Sequence>
  <Series.Sequence durationInFrames={60}>
    <Outro />
  </Series.Sequence>
</Series>
```

---

## Rendering

```bash
# Preview in browser (live Studio)
npm run dev

# Render to MP4
npx remotion render src/Root.tsx MyVideo out/video.mp4

# Render a single frame as PNG (to check one moment)
npx remotion still src/Root.tsx MyVideo --frame=30 out/frame.png
```
