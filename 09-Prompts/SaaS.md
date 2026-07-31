# Prompt: SaaS product marketing site

```
Create a SaaS marketing homepage: hero, social proof strip, feature sections,
pricing table, footer — in the style of Linear.

Stack: Next.js App Router, Tailwind v4, Motion.dev, shadcn/ui + MagicUI for pricing table
and testimonial components, Lenis for scroll feel.

Requirements:
- Hero: product screenshot or short looping product demo video (MP4/WebM, not GIF —
  see 08-Optimization/Video.md), not a 3D scene — SaaS sites should show the real product
- Logo marquee (MagicUI Marquee) for social proof
- Feature sections alternate text/visual sides, each revealing independently on scroll
- Pricing table with an animated toggle (monthly/annual) using Motion.dev layout animation
- Testimonial section using a real quote + avatar pattern, not generic placeholder text
- Fully responsive pricing table (stacks to single column on mobile, not horizontal scroll)
- Accessible: proper heading hierarchy, focus-visible states on every interactive element

Avoid:
- 3D hero (adds load time without adding SaaS-buyer-relevant information — reserve 3D
  for product categories where a literal object needs showing, per 06-3D/R3F.md guidance)
- More than 3 pricing tiers visible without a toggle/expand

Follow production-quality architecture: pricing data as a typed config object, not
hardcoded JSX per tier.
```
