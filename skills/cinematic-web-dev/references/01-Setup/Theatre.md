# Theatre.js

**What it is:** A motion-design/animation library with a visual timeline editor (Studio) that can drive R3F scene properties, camera moves, and DOM values with keyframes.

**Why use it:** Gives you After-Effects-style keyframing for 3D sequences instead of hand-coding every camera move and object transition in code — designers can tweak timing visually.

**When to use it:** Multi-step 3D sequences (camera flythrough across sections, product assembly animations), scroll-scrubbed 3D storytelling where precise keyframe control matters more than physics.

**When to avoid:** Simple one-shot reveals — that's Motion.dev's job, Theatre.js is overkill for a single fade-in.

## Install

```bash
npm install @theatre/core @theatre/studio @theatre/r3f
```

## Minimal example

```tsx
'use client'
import { getProject } from '@theatre/core'
import studio from '@theatre/studio'
import { SheetProvider, editable as e } from '@theatre/r3f'
import { Canvas } from '@react-three/fiber'

if (process.env.NODE_ENV === 'development') studio.initialize()

const project = getProject('CinematicSite')
const sheet = project.sheet('Hero')

export default function Scene() {
  return (
    <Canvas>
      <SheetProvider sheet={sheet}>
        <e.mesh theatreKey="Box">
          <boxGeometry />
          <meshStandardMaterial color="orange" />
        </e.mesh>
      </SheetProvider>
    </Canvas>
  )
}
```

Drive the sheet's playback position from scroll progress (pair with Motion.dev's `useScroll` or Scrollama — see `07-Storytelling/`):

```tsx
sheet.sequence.position = scrollProgress * sheet.sequence.pointer.length
```

## Common mistakes

- Shipping `@theatre/studio` (the editor UI) to production — it's a dev-only dependency; dynamically import and gate it behind `NODE_ENV === 'development'`.
- Not exporting the animated state JSON after finishing edits in Studio — the state lives in browser storage until exported and committed to the project file.
- Driving the sequence position every frame with an unthrottled scroll listener — batch through `requestAnimationFrame` or Lenis's scroll callback instead.

## Official links

- Docs: https://www.theatrejs.com/docs/latest
- GitHub: https://github.com/theatre-js/theatre
