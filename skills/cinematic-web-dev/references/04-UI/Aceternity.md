# Aceternity UI

**What it is:** A Tailwind + Framer Motion component library aimed specifically at landing-page "hero moment" components — 3D card hover effects, spotlight effects, animated gradient backgrounds, timeline/bento layouts.

**When to use it:** Landing page hero sections, feature showcases wanting a strong visual anchor (spotlight cards, 3D tilt cards, animated tabs).

**When to avoid:** Same rule as MagicUI/ReactBits — a details/hero-moment library, not a full design system; don't build an entire app's component set from it.

## Install

Copy-paste per component from https://ui.aceternity.com, or via shadcn-compatible CLI where available:

```bash
npx shadcn@latest add "https://ui.aceternity.com/registry/spotlight.json"
```

## Common mistakes

- Stacking multiple Aceternity "hero moment" effects (3D tilt + spotlight + animated gradient) in the same viewport — each is designed to be *the* focal effect; combining several reads as noisy rather than premium.
- Not checking bundle impact — several Aceternity components use `framer-motion`/`motion` directly with fairly heavy per-frame transforms; profile on a mid-tier mobile device before shipping.

## Official links

- https://ui.aceternity.com
