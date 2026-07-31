# Pricing table template

Data-driven pricing table with animated monthly/annual toggle.

```tsx
// components/sections/Pricing.tsx
'use client'
import { motion } from 'motion/react'
import { useState } from 'react'

const plans = [
  { name: 'Starter', monthly: 19, annual: 15, features: ['1 project', 'Community support'] },
  { name: 'Pro', monthly: 49, annual: 39, features: ['Unlimited projects', 'Priority support', 'Analytics'] },
] as const

export function Pricing() {
  const [annual, setAnnual] = useState(true)

  return (
    <section className="px-6 lg:px-16 py-24">
      <div className="flex items-center justify-center gap-3 mb-12">
        <span className={!annual ? 'font-medium' : 'text-neutral-500'}>Monthly</span>
        <button
          onClick={() => setAnnual((a) => !a)}
          className="relative w-12 h-6 rounded-full bg-neutral-200"
          aria-label="Toggle billing period"
        >
          <motion.div
            className="absolute top-0.5 h-5 w-5 rounded-full bg-brand"
            animate={{ left: annual ? '1.5rem' : '0.125rem' }}
            transition={{ type: 'spring', stiffness: 500, damping: 30 }}
          />
        </button>
        <span className={annual ? 'font-medium' : 'text-neutral-500'}>Annual</span>
      </div>

      <div className="grid sm:grid-cols-2 gap-6 max-w-2xl mx-auto">
        {plans.map((plan) => (
          <div key={plan.name} className="rounded-2xl border p-8">
            <h3 className="text-lg font-medium">{plan.name}</h3>
            <p className="mt-4 text-4xl font-medium">
              ${annual ? plan.annual : plan.monthly}
              <span className="text-base text-neutral-500 font-normal">/mo</span>
            </p>
            <ul className="mt-6 space-y-2 text-sm text-neutral-600">
              {plan.features.map((f) => <li key={f}>{f}</li>)}
            </ul>
          </div>
        ))}
      </div>
    </section>
  )
}
```

## Notes

- Plans live as typed data (`plans` array), not hardcoded per-card JSX — see `09-Prompts/SaaS.md`.
- Grid stacks to single column below `sm:` — never horizontal-scroll a pricing table on mobile.
- Toggle uses a spring transition, not a duration-based one — springs feel more "physical" for state toggles like this.
