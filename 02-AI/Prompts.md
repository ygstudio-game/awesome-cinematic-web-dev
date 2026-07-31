# Prompt discipline for cinematic UI generation

Ready-to-use, fully-written prompts live in `09-Prompts/`. This file covers the *pattern* behind writing your own.

## The structure that works

```
[Role / quality bar]
[Exact stack constraint]
[Concrete requirements list]
[Explicit exclusions]
[Architecture expectation]
```

Example skeleton:

```
Create a [section type] with [reference quality bar, e.g. "Apple/Linear-quality"].

Stack:
- [Next.js / R3F / Motion.dev / Lenis — name exactly what's in the project]

Requirements:
- [functional requirements]
- [responsive/mobile behavior]
- [performance constraints: lazy loaded, one canvas, capped dpr]
- [accessibility: prefers-reduced-motion, keyboard/focus]

Avoid:
- [GSAP unless necessary]
- [anything not in the agreed stack]

Follow production-quality architecture: typed props, no inline magic numbers for easing/timing (pull from shared constants), split into composable subcomponents.
```

## Why exclusions matter as much as requirements

Generic prompts ("make it cinematic and premium") tend to regress to the mean — centered hero, three feature cards, soft gradient blob, generic sans-serif. Naming the *specific* reference (Apple/Stripe/Linear) and the *specific* exclusions (no GSAP, no generic gradient blobs, no stock illustration) is what actually shifts output away from AI-default UI. See `09-Prompts/` for the fully worked versions per site type.

## Iterating

Don't ask for a whole page in one shot. Build hero → next section → next section, reviewing each in the browser (use Playwright MCP, `03-MCP/Playwright.md`) before continuing — a bad structural decision in the hero compounds if every following section is generated to match it.
