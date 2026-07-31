# Drei

**What it is:** The standard helper library for React Three Fiber — pre-built abstractions for cameras, controls, environment/HDRI lighting, loaders, text, and performance helpers (`Bounds`, `Preload`, `PerformanceMonitor`) that would otherwise be raw Three.js boilerplate.

**Why use it:** Nearly every non-trivial R3F scene needs at least `<Environment>`, `<OrbitControls>` or `<useGLTF>` — Drei is the de facto standard companion, not optional.

## Install

Installed together with R3F (see `01-Setup/R3F.md`):

```bash
npm install @react-three/drei
```

## Useful helpers for cinematic sites

```tsx
import { Environment, useGLTF, Preload, PerformanceMonitor, Html } from '@react-three/drei'

// Studio-quality lighting in one line
<Environment preset="studio" />

// Preload the next section's model while current one is visible
useGLTF.preload('/models/product-v2.glb')

// Auto-adjust quality based on measured frame rate
<PerformanceMonitor onDecline={() => setDpr(1)} />

// Overlay DOM content anchored to a 3D point (e.g. a feature callout)
<Html position={[1, 0.5, 0]}>Feature label</Html>
```

## Common mistakes

- Loading `Environment` with a large default HDRI on every page load — use `preset` (built-in, small) unless you specifically need a custom HDRI, and if so, compress it.
- Not using `PerformanceMonitor` on scenes meant to run on a wide range of devices — a scene tuned only on a dev machine's GPU can drop to single-digit fps on a mid-tier phone with no fallback.

## Official links

- https://github.com/pmndrs/drei
