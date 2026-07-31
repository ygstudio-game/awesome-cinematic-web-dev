# Lenis

**What it is:** A smooth-scroll library — replaces native scroll with an eased, interpolated scroll that feels weighty/premium (the scroll feel on most Awwwards-tier sites).

**Why use it:** Native scroll is instant and linear; Lenis adds inertia and easing, and exposes scroll progress as a value other libraries (Motion.dev, ScrollyVideo, Theatre.js) can subscribe to for perfectly synced scroll-driven animation.

**When to use it:** Any site doing scroll-linked animation, parallax, or scrollytelling. Skip it for content-heavy sites (blogs, docs) where users expect native scroll behavior and scroll-jacking feels intrusive.

## Install

```bash
npm install lenis
```

## Setup (Next.js App Router)

```tsx
// components/SmoothScroll.tsx
'use client'
import { ReactLenis } from 'lenis/react'

export function SmoothScroll({ children }: { children: React.ReactNode }) {
  return (
    <ReactLenis root options={{ lerp: 0.1, duration: 1.2 }}>
      {children}
    </ReactLenis>
  )
}
```

Wrap it around `{children}` in `app/layout.tsx`.

Sync with Motion.dev's scroll hooks:

```tsx
import { useLenis } from 'lenis/react'

useLenis(({ scroll, progress }) => {
  // drive Theatre.js sequence position, ScrollyVideo frame, etc.
})
```

## Common mistakes

- Enabling Lenis globally on a page with native anchor links (`#section`) without calling `lenis.scrollTo()` — anchor jumps will fight the smooth-scroll engine.
- Not disabling Lenis under `prefers-reduced-motion` — eased scroll is itself a motion effect; check the media query and fall back to native scroll.
- Nesting scrollable regions (e.g. a modal with its own scroll) inside a Lenis root without excluding them — Lenis intercepts wheel events globally by default.

## Official links

- Docs/GitHub: https://github.com/darkroomengineering/lenis
