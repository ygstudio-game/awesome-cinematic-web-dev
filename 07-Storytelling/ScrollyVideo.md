# ScrollyVideo.js

**What it is:** Syncs video playback frame-by-frame with scroll position — scrolling down plays the video forward, scrolling up plays it backward, at whatever pace the user scrolls.

**Why use it:** This is the single most common "how did they do that" effect on premium product sites (Apple product pages being the canonical example) — a product assembly or rotation that plays exactly in sync with scroll, rather than autoplaying independently of the user.

**When to use it:** Product reveal/assembly sequences, "how it works" walkthroughs, hero sections where a 3D-rendered animation (exported as video, not run live) needs to feel scroll-driven without the cost of a live 3D scene.

**When to prefer live R3F + Theatre.js instead:** If you need real interactivity (rotate/zoom on the object) rather than a fixed camera path — video is a fixed, pre-rendered path; R3F is a live scene.

## Install

```bash
npm install scrollyvideo
```

## Minimal example

```tsx
'use client'
import { useEffect, useRef } from 'react'
import ScrollyVideo from 'scrollyvideo'

export function ProductReveal() {
  const containerRef = useRef<HTMLDivElement>(null)

  useEffect(() => {
    if (!containerRef.current) return
    const sv = new ScrollyVideo({
      scrollyVideoContainer: containerRef.current,
      src: '/videos/product-reveal.mp4',
      transitionSpeed: 8,
      sticky: true,
    })
    return () => sv.destroy()
  }, [])

  return <div ref={containerRef} style={{ height: '400vh' }} />
}
```

## Common mistakes

- Using a highly compressed/low-bitrate video for scroll-scrubbing — since ScrollyVideo seeks to arbitrary frames (not just plays sequentially), heavy inter-frame compression (long GOP) causes visible stutter on seek. Encode with a shorter keyframe interval for scrub-heavy footage — see `08-Optimization/Video.md`.
- Not setting an explicit scroll-distance wrapper (`height: 400vh` above) — without scroll runway, the whole video plays within a single viewport's worth of scrolling, too fast to read as cinematic.
- Autoplaying the same video traditionally *and* wiring it to ScrollyVideo — pick one; ScrollyVideo takes over playback control entirely.

## Official links

- GitHub: https://github.com/scrollytellers/ScrollyVideo
