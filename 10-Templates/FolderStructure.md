# Recommended project folder structure

```
src/
├── app/
│   ├── layout.tsx            # SmoothScroll (Lenis) wraps children here
│   ├── template.tsx          # Motion.dev page-transition wrapper
│   ├── page.tsx               # homepage, composes sections below
│   └── globals.css            # Tailwind @theme tokens
│
├── components/
│   ├── ui/                    # shadcn/MagicUI/21st.dev components (copy-in, owned)
│   ├── sections/               # Hero, FeatureGrid, Pricing, Contact, Footer
│   ├── three/                  # R3F scenes: Hero3D.tsx, ProductScene.tsx, CameraRig.tsx
│   ├── motion/                 # shared Motion.dev variants/constants
│   └── storytelling/            # ScrollyVideo/Scrollama wrapper components
│
├── lib/
│   ├── theatre/                 # Theatre.js project/sheet definitions
│   ├── constants.ts             # shared easing curves, durations, breakpoints
│   └── utils.ts
│
├── public/
│   ├── models/                  # optimized .glb (06-3D/Blender.md)
│   ├── videos/                   # encoded mp4/webm (08-Optimization/Video.md)
│   └── images/
│
└── CLAUDE.md                     # project conventions (02-AI/Claude.md)
```

## Why this shape

- `components/three/` and `components/storytelling/` are separated from `components/sections/` because they're the client-only, `next/dynamic`-loaded pieces — keeping them physically separate makes the lazy-loading boundary obvious at a glance.
- `lib/constants.ts` centralizes easing curves/durations so every Motion.dev/Theatre.js/GSAP usage across the codebase stays visually consistent instead of each component inventing its own timing.
- `public/models` and `public/videos` store only the *optimized* output of the pipelines in `06-3D/Blender.md` and `08-Optimization/Video.md` — keep raw/source files outside the repo or in a separate assets branch/LFS to avoid bloating the repo.

## Common mistakes

- Putting R3F/Theatre.js components directly in `app/` — forces them into the server component tree by default; keep them in `components/three/` and import via `next/dynamic`.
- No `lib/constants.ts` — leads to slightly different easing curves scattered across components, which reads as inconsistent polish even when each individual animation is well-crafted.
