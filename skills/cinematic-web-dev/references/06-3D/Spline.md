# Spline (optional)

**What it is:** A visual 3D design tool (like Figma, but for 3D scenes) that exports scenes runnable in the browser via `@splinetool/react-spline`.

**Why it's optional here:** Spline scenes are heavier and less controllable in code than a hand-built R3F scene — every camera/animation tweak requires going back into the Spline editor rather than editing code directly alongside the rest of your React app.

**When to actually use it:**
- Marketing/landing pages where a designer (non-developer) needs to iterate on the 3D scene independently.
- A one-off interactive scene that doesn't need deep integration with app state.

**When to use R3F directly instead:** Anything that needs to react to real app data, be sequenced precisely with Theatre.js, or hit a tight performance budget — Spline's exported scenes carry more overhead and less fine-grained control.

## Install

```bash
npm install @splinetool/react-spline @splinetool/runtime
```

## Minimal example

```tsx
'use client'
import Spline from '@splinetool/react-spline'

export default function SplineHero() {
  return <Spline scene="https://prod.spline.design/xxxxx/scene.splinecode" />
}
```

## Common mistakes

- Embedding a Spline scene as the primary hero *and* running a separate R3F canvas elsewhere on the page — violates the one-active-canvas rule (`README.md`) and doubles WebGL overhead.
- Not lazy-loading it (`next/dynamic`, `ssr:false`) — same rule as any R3F canvas, see `01-Setup/NextJS.md`.

## Official links

- https://spline.design
