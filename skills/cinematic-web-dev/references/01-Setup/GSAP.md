# GSAP (use only if necessary)

**What it is:** The most mature JS animation engine, with `ScrollTrigger` for scroll-scrubbed timelines and best-in-class SVG morphing (`MorphSVG`, paid plugin).

**Why it's opt-in here:** Motion.dev covers the vast majority of cinematic-site needs with a smaller bundle and cleaner React integration. Running both GSAP and Motion.dev means two animation engines fighting for the same frame budget — only add GSAP when you hit something Motion.dev genuinely can't do.

**When to actually reach for it:**
- Complex SVG path morphing between arbitrary shapes.
- Multi-element timeline scrubbing tied precisely to scroll position, with pinning (`ScrollTrigger.pin`).
- Porting an existing GSAP-based design/animation spec from a motion designer who works in GSAP.

**When not to:** Simple reveals, hover states, page transitions — that's Motion.dev's job (`01-Setup/Motion.md`).

## Install

```bash
npm install gsap
```

## Minimal example (scroll-pinned section)

```tsx
'use client'
import { useEffect, useRef } from 'react'
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

export function PinnedSection() {
  const ref = useRef<HTMLDivElement>(null)

  useEffect(() => {
    const ctx = gsap.context(() => {
      gsap.to('.panel', {
        xPercent: -300,
        ease: 'none',
        scrollTrigger: {
          trigger: ref.current,
          pin: true,
          scrub: 1,
          end: '+=3000',
        },
      })
    }, ref)
    return () => ctx.revert()
  }, [])

  return <div ref={ref}>...</div>
}
```

## Common mistakes

- Loading GSAP *and* using Lenis/Motion.dev scroll listeners on the same scroll source without reconciling them — `ScrollTrigger` needs to be told about Lenis via `ScrollTrigger.scrollerProxy` or `lenis.on('scroll', ScrollTrigger.update)`.
- Not calling `gsap.context().revert()` on unmount in React — leaks ScrollTrigger instances across route changes in Next.js.
- Reaching for GSAP by default instead of Motion.dev "because it's more powerful" — more power here means more bundle size and more footguns for cases you don't need.

## Official links

- Docs: https://gsap.com/docs/v3/
- GitHub: https://github.com/greensock/GSAP
