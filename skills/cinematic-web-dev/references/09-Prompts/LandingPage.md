# Prompt: General cinematic landing page

```
Create a landing page hero + first two sections in the style of Linear/Stripe —
restrained, confident, fast-feeling.

Stack: Next.js App Router, Tailwind v4, Motion.dev, Lenis, MagicUI/21st.dev components.

Requirements:
- Hero: headline, subhead, single primary CTA, one supporting visual (not literal
  product screenshot — an abstract animated element from MagicUI/ReactBits)
- Staggered reveal on scroll into view (05-Animation/Motion.md stagger pattern)
- Animated nav that condenses on scroll
- Section 2: feature grid using a MagicUI bento layout, each card revealing on scroll
- Dark and light mode both fully styled, not just inverted colors
- Mobile-first: build and verify the mobile layout before the desktop layout
- prefers-reduced-motion fallback on every animated element

Avoid:
- Auto-playing carousels, more than one competing CTA in the hero,
  decorative animation that doesn't reinforce the content's meaning

Follow production-quality architecture: composable sections, shared design tokens
from Tailwind @theme (01-Setup/Tailwind.md), no inline magic numbers for timing/easing.
```
