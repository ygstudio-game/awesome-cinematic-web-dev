# React Three Fiber — see 01-Setup/R3F.md for install/basics

This file covers the camera-and-scroll pattern used for product showcases and hero sections.

## Scroll-driven camera move

```tsx
'use client'
import { Canvas, useFrame } from '@react-three/fiber'
import { useRef } from 'react'
import * as THREE from 'three'

function CameraRig({ scrollProgress }: { scrollProgress: React.MutableRefObject<number> }) {
  useFrame(({ camera }) => {
    const p = scrollProgress.current
    camera.position.lerp(new THREE.Vector3(0, p * 2, 5 - p * 2), 0.05)
    camera.lookAt(0, 0, 0)
  })
  return null
}

export default function ProductScene() {
  const scrollProgress = useRef(0)
  // update scrollProgress.current from Lenis (01-Setup/Lenis.md) in a parent effect
  return (
    <Canvas dpr={[1, 2]} frameloop="demand">
      <CameraRig scrollProgress={scrollProgress} />
      {/* model */}
    </Canvas>
  )
}
```

`frameloop="demand"` only re-renders on state change or `invalidate()` calls — pair with `invalidate()` inside the scroll handler for a scroll-driven scene that doesn't burn frames when idle.

## Common mistakes

See `01-Setup/R3F.md` — the same rules (one canvas, capped dpr, lazy assets) apply; this file only adds the camera-rig pattern.

## Official links

- https://r3f.docs.pmnd.rs/
