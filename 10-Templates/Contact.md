# Contact section template

```tsx
// components/sections/Contact.tsx
'use client'
import { motion, useReducedMotion } from 'motion/react'
import { useState } from 'react'

export function Contact() {
  const [status, setStatus] = useState<'idle' | 'sending' | 'sent'>('idle')
  const shouldReduceMotion = useReducedMotion()

  async function handleSubmit(e: React.FormEvent<HTMLFormElement>) {
    e.preventDefault()
    setStatus('sending')
    const form = new FormData(e.currentTarget)
    await fetch('/api/contact', { method: 'POST', body: form })
    setStatus('sent')
  }

  return (
    <section className="px-6 lg:px-16 py-24 max-w-xl mx-auto">
      <motion.h2
        initial={{ opacity: 0, y: shouldReduceMotion ? 0 : 16 }}
        whileInView={{ opacity: 1, y: 0 }}
        viewport={{ once: true }}
        className="text-3xl font-medium"
      >
        Let's talk
      </motion.h2>

      {status === 'sent' ? (
        <p className="mt-8 text-neutral-600">Thanks — we'll be in touch shortly.</p>
      ) : (
        <form onSubmit={handleSubmit} className="mt-8 space-y-4">
          <input
            name="email"
            type="email"
            required
            placeholder="you@company.com"
            className="w-full rounded-lg border px-4 py-3 focus-visible:outline-2 focus-visible:outline-brand"
          />
          <textarea
            name="message"
            required
            rows={4}
            placeholder="What are you building?"
            className="w-full rounded-lg border px-4 py-3 focus-visible:outline-2 focus-visible:outline-brand"
          />
          <button
            type="submit"
            disabled={status === 'sending'}
            className="px-6 py-3 rounded-full bg-brand text-white font-medium disabled:opacity-50"
          >
            {status === 'sending' ? 'Sending...' : 'Send message'}
          </button>
        </form>
      )}
    </section>
  )
}
```

## Notes

- `focus-visible:outline` is explicit, not left to browser default — a detail generic AI-generated forms frequently skip, and one of the concrete things a UX-rigor skill (`02-AI/Skills.md`) should catch.
- Reveal respects `useReducedMotion` directly rather than relying on the `whileInView` default.
- Real submission handling (`/api/contact`) is a Next.js route handler — wire to your actual email/CRM provider; this template only shows the client-side contract.
