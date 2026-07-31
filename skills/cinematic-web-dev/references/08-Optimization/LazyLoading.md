# Lazy loading

**The rule:** Preload only the assets needed for the *next* section the user will realistically reach — never the whole page's assets up front.

## Code-splitting heavy components (Next.js)

```tsx
import dynamic from 'next/dynamic'

const Hero3D = dynamic(() => import('@/components/Hero3D'), {
  ssr: false,
  loading: () => <HeroSkeleton />,
})
```

Any R3F canvas, ScrollyVideo instance, or Theatre.js-driven scene should be behind `next/dynamic` with `ssr: false` — these are all client-only and otherwise bloat the initial server-rendered bundle.

## Loading assets just ahead of when they're needed

```tsx
import { useGLTF } from '@react-three/drei'

// Preload section-2's model while section-1 is still on screen
useEffect(() => {
  const observer = new IntersectionObserver(([entry]) => {
    if (entry.isIntersecting) useGLTF.preload('/models/section-2.glb')
  }, { rootMargin: '200% 0px' }) // trigger well before it's in view
  observer.observe(section1Ref.current!)
  return () => observer.disconnect()
}, [])
```

## Route-level splitting

Next.js does this automatically per route — but within a single long-scrolling page (common for cinematic sites, which are often one long page rather than many routes), you're responsible for splitting *within* the page yourself using the patterns above.

## Common mistakes

- Loading every section's video/3D assets at page mount "to avoid pop-in later" — this is exactly backwards; it delays the metrics that matter (LCP, TTI) for content most users won't even scroll to.
- Using `IntersectionObserver` with a `rootMargin` of `0px` for preloading — by the time the element is actually visible, it's too late to preload; use a large positive `rootMargin` to trigger early.
- Forgetting to also lazy-load the *code* (not just data/assets) for a section — a component importing `three`/`@theatre/core` at the top of a file that's part of the main bundle pulls those libraries in regardless of whether the section ever renders.
