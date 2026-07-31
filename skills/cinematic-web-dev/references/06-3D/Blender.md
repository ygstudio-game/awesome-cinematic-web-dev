# Blender → web pipeline

**What it is:** The open-source 3D modeling tool used to author models/scenes that get exported as `.glb`/`.gltf` for use in React Three Fiber.

**Why it matters for a cinematic site:** Web-ready assets need to be modeled and exported with performance in mind from the start — a model built without web constraints in mind (unoptimized topology, huge textures, unnecessary hierarchy) will be slow no matter how well the R3F/Drei code is written.

## Pipeline

```
Model in Blender
  → keep poly count reasonable (thousands, not millions, for a hero object)
  → bake materials to as few texture sets as possible
  → File → Export → glTF 2.0 (.glb, binary — single file, embeds textures)
  → compress with gltf-transform
  → import via useGLTF in R3F
```

## Compress after export

```bash
npm install -g @gltf-transform/cli
gltf-transform optimize model.glb model-optimized.glb --texture-compress webp
```

This applies Draco/Meshopt geometry compression and re-encodes textures — often a 70-90% size reduction with no visible quality loss for web viewing distances.

## Load in R3F

```tsx
import { useGLTF } from '@react-three/drei'

function Product() {
  const { scene } = useGLTF('/models/product-optimized.glb')
  return <primitive object={scene} />
}
useGLTF.preload('/models/product-optimized.glb')
```

## Common mistakes

- Exporting straight from Blender without running `gltf-transform optimize` — raw exports are frequently 5-20x larger than necessary.
- Baking 4K textures for objects that will only ever render at a few hundred pixels on screen — match texture resolution to actual on-screen size.
- Keeping Blender's full scene hierarchy (empties, unused cameras/lights) in the export — strip to just the geometry/materials you need before exporting.

## Official links

- Blender: https://www.blender.org
- glTF-Transform: https://gltf-transform.dev
