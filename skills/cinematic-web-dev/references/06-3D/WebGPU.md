# WebGPU (future / progressive enhancement)

**What it is:** The successor graphics API to WebGL — lower overhead, compute shader support, better performance ceiling for complex scenes. Three.js has an experimental `WebGPURenderer`.

**Why it's "future" in this handbook:** Browser support is not yet universal (notably still catching up in some Safari/Firefox versions as of this writing) — treat it as a progressive enhancement, not a baseline requirement, for a client-facing marketing/agency site in 2026.

**When to consider it:** Projects specifically pushing the boundary of in-browser 3D (high object counts, custom compute-shader effects) where you control the audience's browser environment (internal tools, tech-forward audience) more than a general public marketing site.

## Trying it

```bash
npm install three@latest
```

```tsx
import { WebGPURenderer } from 'three/webgpu'
// R3F: <Canvas gl={(props) => new WebGPURenderer(props)}>
```

Always feature-detect and fall back to the standard WebGL renderer:

```ts
const supported = 'gpu' in navigator
```

## Common mistakes

- Shipping WebGPU-only code paths to a general audience without a WebGL fallback — will hard-fail for a meaningful chunk of visitors.
- Chasing WebGPU for a project where WebGL already meets the performance budget — added complexity without a corresponding user-facing benefit.

## Official links

- https://threejs.org/docs/#manual/en/introduction/How-to-use-WebGPU
