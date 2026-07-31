# Hero section template

Composable pattern combining Motion.dev text reveal + lazy-loaded 3D/video visual.

```tsx
// components/sections/Hero.tsx
'use client'
import dynamic from 'next/dynamic'
import { motion } from 'motion/react'

const HeroVisual = dynamic(() => import('@/components/three/Hero3D'), {
  ssr: false,
  loading: () => <div className="aspect-square animate-pulse bg-neutral-900/5 rounded-3xl" />,
})

export function Hero() {
  return (
    <section className="grid lg:grid-cols-2 gap-12 items-center min-h-screen px-6 lg:px-16">
      <div>
        <motion.h1
          initial={{ opacity: 0, y: 24 }}
          animate={{ opacity: 1, y: 0 }}
          transition={{ duration: 0.7, ease: [0.16, 1, 0.3, 1] }}
          className="text-5xl lg:text-7xl font-display font-medium tracking-tight"
        >
          Headline that states the outcome, not the feature.
        </motion.h1>
        <motion.p
          initial={{ opacity: 0, y: 24 }}
          animate={{ opacity: 1, y: 0 }}
          transition={{ duration: 0.7, delay: 0.1, ease: [0.16, 1, 0.3, 1] }}
          className="mt-6 text-lg text-neutral-500 max-w-md"
        >
          One sentence of supporting context. No more.
        </motion.p>
        <motion.div
          initial={{ opacity: 0, y: 24 }}
          animate={{ opacity: 1, y: 0 }}
          transition={{ duration: 0.7, delay: 0.2, ease: [0.16, 1, 0.3, 1] }}
          className="mt-8"
        >
          <a href="#cta" className="inline-flex px-6 py-3 rounded-full bg-brand text-white font-medium">
            Primary action
          </a>
        </motion.div>
      </div>
      <HeroVisual />
    </section>
  )
}
```

## Notes

- Text reveals animate on mount (`animate`, not `whileInView`) since the hero is above the fold by definition — no observer needed.
- The 3D visual is the only lazy-loaded piece; text should never wait on it, which is why they're structured as siblings, not the visual gating the text.
- Swap `HeroVisual` for a `ScrollyVideo`-based component on mobile per `09-Prompts/AppleStyle.md` guidance if the R3F scene is too heavy for the target device tier.
