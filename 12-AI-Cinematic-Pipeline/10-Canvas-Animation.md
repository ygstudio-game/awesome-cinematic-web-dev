# Canvas Animation

**What it is:** Rendering the extracted frame sequence (`09-Frame-Extraction.md`) to a `<canvas>` element, drawing whichever frame corresponds to current scroll position — a scroll-scrubbed animation built from discrete images instead of a video element.

**Why this instead of `ScrollyVideo.js` (`07-Storytelling/ScrollyVideo.md`, root):** ScrollyVideo seeks within an actual video file, which depends on the browser's video decoder handling arbitrary-frame seeks smoothly (mitigated there by a short GOP encode). A canvas frame sequence sidesteps video seeking entirely — you're just drawing a pre-decoded image per scroll position — which can be smoother on lower-end devices, and supports true alpha transparency per frame (WebP/PNG) for compositing over other page content, which video can't do natively in the browser.

**Trade-off:** More total HTTP requests (one per frame) versus one video file — mitigate with the preload strategy below and `08-Optimization/LazyLoading.md` (root).

## Minimal implementation (React)

```tsx
'use client'
import { useEffect, useRef, useState } from 'react'

type Manifest = { frameCount: number; fps: number; width: number; height: number; framePattern: string }

export function CanvasSequence({ manifestUrl }: { manifestUrl: string }) {
  const canvasRef = useRef<HTMLCanvasElement>(null)
  const framesRef = useRef<HTMLImageElement[]>([])
  const [manifest, setManifest] = useState<Manifest | null>(null)

  useEffect(() => {
    fetch(manifestUrl).then((r) => r.json()).then((m: Manifest) => {
      setManifest(m)
      framesRef.current = Array.from({ length: m.frameCount }, (_, i) => {
        const img = new Image()
        img.src = m.framePattern.replace('%04d', String(i + 1).padStart(4, '0'))
        return img
      })
    })
  }, [manifestUrl])

  useEffect(() => {
    if (!manifest) return
    const canvas = canvasRef.current!
    const ctx = canvas.getContext('2d')!
    canvas.width = manifest.width
    canvas.height = manifest.height

    function render() {
      const scrollProgress = window.scrollY / (document.body.scrollHeight - window.innerHeight)
      const frameIndex = Math.min(
        manifest!.frameCount - 1,
        Math.floor(scrollProgress * manifest!.frameCount)
      )
      const frame = framesRef.current[frameIndex]
      if (frame?.complete) ctx.drawImage(frame, 0, 0, canvas.width, canvas.height)
    }

    window.addEventListener('scroll', render, { passive: true })
    render()
    return () => window.removeEventListener('scroll', render)
  }, [manifest])

  return <canvas ref={canvasRef} className="w-full h-full" />
}
```

Route scroll position through Lenis (`01-Setup/Lenis.md`, root) rather than a raw `scroll` listener once Lenis is in the project, same rule as everywhere else scroll position drives animation.

## Preloading strategy

Loading all frames eagerly defeats lazy-loading discipline (`08-Optimization/LazyLoading.md`, root). Load the first ~10% of frames eagerly (enough for the section to render immediately on scroll-in), then load the rest progressively while the user is scrolling toward them:

```tsx
const eagerCount = Math.ceil(manifest.frameCount * 0.1)
framesRef.current.slice(0, eagerCount).forEach((img) => { img.loading = 'eager' })
```

## Common mistakes

- Loading every frame image eagerly on mount — for a few-hundred-frame sequence this can be tens of megabytes fetched before the user has scrolled at all; preload progressively instead.
- Driving `render()` off raw `scroll` events without `{ passive: true }` or a `requestAnimationFrame` throttle — causes jank on scroll-heavy pages; throttle via rAF if profiling shows main-thread cost.
- Using this technique for a sequence with only a handful of frames — that's just a regular sprite/keyframe animation; canvas-sequence overhead is only worth it for genuinely video-length sequences (dozens to hundreds of frames).
