# Theatre.js — deeper sequencing patterns

See `01-Setup/Theatre.md` for install/basics. This file covers driving a Theatre.js sequence from scroll, the primary pattern for cinematic 3D storytelling.

## Scroll-scrubbed sequence (Lenis + Theatre.js)

```tsx
'use client'
import { useLenis } from 'lenis/react'
import { useRef } from 'react'
import { getProject } from '@theatre/core'

const project = getProject('CinematicSite')
const sheet = project.sheet('ProductReveal')

export function ScrollDrivenScene({ children }: { children: React.ReactNode }) {
  const sectionRef = useRef<HTMLDivElement>(null)

  useLenis(() => {
    const el = sectionRef.current
    if (!el) return
    const rect = el.getBoundingClientRect()
    const progress = Math.min(1, Math.max(0, -rect.top / (rect.height - window.innerHeight)))
    sheet.sequence.position = progress * sheet.sequence.pointer.length
  })

  return <div ref={sectionRef} style={{ height: '300vh' }}>{children}</div>
}
```

The tall wrapper (`300vh`) gives scroll distance for the sequence to scrub through while the actual visible content stays pinned via CSS (`position: sticky`) inside it.

## Common mistakes

- Not pinning the visual content while its containing section provides scroll distance — without `position: sticky`, the scene scrolls away instead of staying on screen while the sequence plays.
- Computing `sheet.sequence.position` on every native scroll event instead of through Lenis's batched callback — causes stutter; always route through Lenis (`01-Setup/Lenis.md`) once it's in the project.
- Building a Theatre.js sequence without ever testing at the actual target viewport sizes — the "300vh" scroll distance that feels right on desktop can feel radically different on a tall mobile viewport.
