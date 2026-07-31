# Motion.dev — deeper animation patterns

See `01-Setup/Motion.md` for install and basics. This file covers the patterns you'll actually reuse across a cinematic site.

## Staggered section reveal

```tsx
'use client'
import { motion } from 'motion/react'

const container = {
  hidden: {},
  show: { transition: { staggerChildren: 0.12 } },
}
const item = {
  hidden: { opacity: 0, y: 20 },
  show: { opacity: 1, y: 0, transition: { duration: 0.5, ease: [0.16, 1, 0.3, 1] } },
}

export function FeatureGrid({ items }: { items: string[] }) {
  return (
    <motion.div variants={container} initial="hidden" whileInView="show" viewport={{ once: true }}>
      {items.map((t) => <motion.div key={t} variants={item}>{t}</motion.div>)}
    </motion.div>
  )
}
```

## Shared layout transitions (e.g. tab indicator, expanding card)

```tsx
<motion.div layoutId="active-pill" className="pill" />
```

Motion.dev automatically animates position/size changes for any element sharing a `layoutId` across renders — this is how Linear-style animated nav underlines/pills work.

## Page transitions (App Router)

```tsx
// app/template.tsx
'use client'
import { motion } from 'motion/react'

export default function Template({ children }: { children: React.ReactNode }) {
  return (
    <motion.div initial={{ opacity: 0 }} animate={{ opacity: 1 }} exit={{ opacity: 0 }}>
      {children}
    </motion.div>
  )
}
```

`template.tsx` re-mounts on every navigation (unlike `layout.tsx`), which is what makes enter animations re-trigger per route.

## `prefers-reduced-motion` gate

```tsx
import { useReducedMotion } from 'motion/react'

const shouldReduceMotion = useReducedMotion()
const variants = shouldReduceMotion
  ? { hidden: { opacity: 0 }, show: { opacity: 1 } }
  : { hidden: { opacity: 0, y: 20 }, show: { opacity: 1, y: 0 } }
```

## Common mistakes

- Using `layoutId` shared across many list items with dynamic keys — causes unexpected shared-layout jumps; scope `layoutId` carefully to genuinely-the-same element.
- Forgetting `template.tsx` re-renders the whole subtree on every nav — heavy data fetching there re-runs each transition; keep data fetching in `layout.tsx`/server components instead.
