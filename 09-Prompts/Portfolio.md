# Prompt: Cinematic portfolio site

```
Create a personal/studio portfolio homepage with a strong cinematic, editorial feel —
reference: Basement Studio, Godly-featured portfolio sites.

Stack: Next.js App Router, Tailwind v4, Motion.dev, Lenis, ScrollyVideo.js for project
reveals, ReactBits/Skiper-style components for text effects (07-Storytelling/Basement.md,
05-Animation/ReactKino.md).

Requirements:
- Full-bleed hero with a single strong visual statement (large type + subtle motion,
  or a ScrollyVideo-driven reveal) rather than a conventional headline+CTA hero
- Project grid where each project reveals via scroll with a distinct transition —
  favor typographic/motion craft over generic card-hover-lift effects
- Custom cursor or magnetic hover detail on project links (ReactBits) — used sparingly,
  once, not on every interactive element
- About/contact section with restrained, confident typography
- prefers-reduced-motion fallback that keeps the site fully navigable and legible,
  not just "less fancy"

Avoid:
- Generic SaaS-style layout patterns (feature grid + pricing table + testimonials) —
  a portfolio should not read as a SaaS landing page
- Overusing scroll-hijacking — reserve continuous scroll-scrub for one flagship moment,
  keep the rest of the page on natural scroll

Follow production-quality architecture: project data as a typed array/CMS-driven,
not hardcoded per project.
```
