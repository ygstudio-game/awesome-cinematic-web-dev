# React Three Fiber

**What it is:** A React renderer for Three.js — write 3D scenes as JSX components instead of imperative Three.js calls.

**Why use it:** Keeps 3D scene graphs declarative and composable with the rest of your React app (props, state, context, suspense all work normally).

**When to use it:** Product showcases, hero sections, interactive backgrounds, camera-driven storytelling.

**When to avoid:** Dashboards, blogs, admin panels, anything where 3D adds no communicative value — it only costs performance budget there.

## Install

```bash
npm install three @react-three/fiber @react-three/drei
npm install -D @types/three
```

## Minimal example (Next.js, client-only)

```tsx
// components/Hero3D.tsx
'use client'
import { Canvas } from '@react-three/fiber'
import { Environment, OrbitControls } from '@react-three/drei'

export default function Hero3D() {
  return (
    <Canvas camera={{ position: [0, 0, 5], fov: 45 }} dpr={[1, 2]}>
      <ambientLight intensity={0.6} />
      <directionalLight position={[3, 3, 3]} intensity={1.2} />
      <mesh>
        <torusKnotGeometry args={[1, 0.3, 128, 32]} />
        <meshStandardMaterial color="#7c5cff" roughness={0.2} metalness={0.6} />
      </mesh>
      <Environment preset="city" />
      <OrbitControls enableZoom={false} />
    </Canvas>
  )
}
```

Load it with `next/dynamic` and `ssr: false` (see `01-Setup/NextJS.md`).

## Common mistakes

- Multiple `<Canvas>` instances on one page → multiple WebGL contexts, tanks performance and can hit browser context limits. Keep one active canvas; swap scene contents inside it.
- Not capping `dpr` → renders at full device pixel ratio on high-DPI phones, wasted GPU work. Use `dpr={[1, 2]}`.
- Loading full-resolution GLTF/texture assets synchronously → use `useGLTF.preload()` selectively and `Suspense` boundaries, only for the next section's assets (see `08-Optimization/LazyLoading.md`).
- Running `useFrame` logic unconditionally when the canvas is off-screen — pause with `frameloop="demand"` or an intersection check.

## Official links

- Docs: https://r3f.docs.pmnd.rs/
- GitHub: https://github.com/pmndrs/react-three-fiber
