# Scrollama

**What it is:** A lightweight scrollytelling library that fires enter/exit/progress events as the user scrolls through defined "steps" — the standard tool behind data-journalism-style scroll narratives (NYT/Pudding-style stories).

**Why use it:** Uses `IntersectionObserver` under the hood rather than continuous scroll-position polling — cheap, reliable step-triggering, complements (doesn't replace) continuous scroll-progress tools like Lenis/Motion's `useScroll`.

**When to use it:** Discrete step-based narratives — "as you scroll past step 3, swap the image and text" — as opposed to continuous scrubbing (that's ScrollyVideo/Theatre.js's job).

## Install

```bash
npm install scrollama
```

## Minimal example (React wrapper)

```tsx
'use client'
import { useEffect, useRef, useState } from 'react'
import scrollama from 'scrollama'

export function ScrollyStory({ steps }: { steps: { title: string; body: string }[] }) {
  const [active, setActive] = useState(0)
  const containerRef = useRef<HTMLDivElement>(null)

  useEffect(() => {
    const scroller = scrollama()
    scroller
      .setup({ step: '.step', offset: 0.6 })
      .onStepEnter(({ index }) => setActive(index))
    window.addEventListener('resize', scroller.resize)
    return () => { scroller.destroy(); window.removeEventListener('resize', scroller.resize) }
  }, [])

  return (
    <div ref={containerRef} className="relative">
      <div className="sticky top-0 h-screen">{/* render steps[active] */}</div>
      {steps.map((s, i) => <div key={i} className="step h-screen">{s.title}</div>)}
    </div>
  )
}
```

## Common mistakes

- Not calling `scroller.resize()` on window resize/content-load changes — step boundaries drift and stop triggering at the intended scroll position.
- Combining Scrollama's step offsets with Lenis smooth scroll without testing — smooth scroll changes the effective scroll velocity through each step; verify triggers still feel right with Lenis enabled.

## Official links

- GitHub: https://github.com/russellsamora/scrollama
