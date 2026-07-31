# Motion.dev (Motion for React, formerly Framer Motion)

**What it is:** The animation library used for page transitions, section reveals, cursor effects, scroll-linked animation, and micro-interactions.

**Why use it:** Declarative, React-native, hardware-accelerated where possible, and handles the 90% case (fade/slide/scale reveals, layout animation, gesture-driven interaction) without the timeline complexity of GSAP.

**When to use it:** Page transitions, on-scroll reveals, hover/tap micro-interactions, shared layout animations, simple scroll-linked parallax.

**When to reach for GSAP instead:** Complex SVG path morphing, precise multi-track timeline scrubbing tied to scroll (see `01-Setup/GSAP.md`) — otherwise stay in Motion.dev to avoid running two animation engines.

## Install

```bash
npm install motion
```

## Minimal example

```tsx
'use client'
import { motion } from 'motion/react'

export function Reveal({ children }: { children: React.ReactNode }) {
  return (
    <motion.div
      initial={{ opacity: 0, y: 24 }}
      whileInView={{ opacity: 1, y: 0 }}
      viewport={{ once: true, margin: '-100px' }}
      transition={{ duration: 0.6, ease: [0.16, 1, 0.3, 1] }}
    >
      {children}
    </motion.div>
  )
}
```

Scroll-linked (parallax) using `useScroll`:

```tsx
'use client'
import { motion, useScroll, useTransform } from 'motion/react'
import { useRef } from 'react'

export function Parallax() {
  const ref = useRef(null)
  const { scrollYProgress } = useScroll({ target: ref, offset: ['start end', 'end start'] })
  const y = useTransform(scrollYProgress, [0, 1], [0, -120])
  return <motion.div ref={ref} style={{ y }}>...</motion.div>
}
```

## Common mistakes

- Animating `top`/`left`/`width` instead of `transform`/`opacity` → forces layout, kills frame rate. Stick to transform-based properties.
- Not setting `viewport={{ once: true }}` on scroll reveals → re-triggers every time the element re-enters view, which reads as jittery rather than cinematic.
- Running heavy `useScroll` transforms on many elements simultaneously on mobile — throttle or simplify below a breakpoint; see `08-Optimization/`.
- Forgetting `prefers-reduced-motion` handling — Motion.dev respects it automatically for some APIs but not custom `useTransform` chains; gate those manually.

## Official links

- Docs: https://motion.dev/docs
- GitHub: https://github.com/motiondivision/motion
