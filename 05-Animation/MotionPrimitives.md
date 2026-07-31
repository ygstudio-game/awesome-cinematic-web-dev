# Motion Primitives

**What it is:** A component library (by the Motion.dev/Framer Motion ecosystem authors) of pre-built, copy-paste animation patterns — text effects, image comparisons, dialogs, accordions — all built on Motion.dev primitives rather than a separate engine.

**Why use it:** Same install/mental-model as Motion.dev itself (no second animation engine), higher-level than hand-rolling every `motion.div` variant — good source for common patterns (animated tooltip, text shimmer, in-view counter) instead of reinventing them.

**When to use it:** Filling in the "small interaction details" layer once your main layout is built with MagicUI/ReactBits/21st.dev — this is a good source for things like animated number counters, text effects, and tooltip/popover motion.

## Install

Copy-paste per component from https://motion-primitives.com, or via CLI:

```bash
npx shadcn@latest add "https://motion-primitives.com/r/text-shimmer.json"
```

## Common mistakes

- Treating it as a full UI kit — it's focused on animation patterns, not layout/structural components; pair with `04-UI/`.

## Official links

- https://motion-primitives.com
