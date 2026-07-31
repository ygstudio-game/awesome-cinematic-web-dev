# Next.js (App Router)

**What it is:** React meta-framework with file-system routing, server components, image/font optimization, and built-in bundling — the foundation layer for the whole stack.

**Why use it:** Everything else in this handbook (Motion.dev, R3F, ScrollyVideo, MCP tooling) assumes a React app. Next.js gives you SSR/SSG for fast first paint, `next/image` for automatic image optimization, and route-level code splitting so heavy 3D/animation code doesn't block pages that don't use it.

**When to use it:** Default choice for almost any project in this handbook — marketing sites, agency sites, SaaS landing pages, portfolios.

**When to avoid:** Pure client-only experiments/prototypes where you don't need routing or SSR — a Vite + React app is lighter and faster to iterate on.

## Install

```bash
npx create-next-app@latest my-cinematic-site
cd my-cinematic-site
```

Recommended prompts when the CLI asks:
- TypeScript: **Yes**
- ESLint: **Yes**
- Tailwind CSS: **Yes**
- `src/` directory: **Yes**
- App Router: **Yes**
- Import alias (`@/*`): **Yes**

```bash
npm run dev
```

## Config notes

- Use `app/` router, not `pages/` — all modern libraries in this handbook (Motion.dev examples, R3F SSR patterns) target App Router.
- Mark any component using `useFrame`, `IntersectionObserver`, `window`, or Motion.dev's `useScroll` with `'use client'` at the top of the file — these libraries are client-only.
- Use `next/dynamic` with `ssr: false` to lazy-load your R3F canvas and any scrollytelling component — see `08-Optimization/LazyLoading.md`.

```tsx
// app/page.tsx
import dynamic from 'next/dynamic'

const Hero3D = dynamic(() => import('@/components/Hero3D'), { ssr: false })

export default function Page() {
  return <Hero3D />
}
```

## Common mistakes

- Importing Three.js/R3F code into a server component → build fails or hydration mismatch. Always `'use client'` + dynamic import with `ssr:false`.
- Leaving `pages/` and `app/` both present after migrating — pick one router.
- Not setting `images.remotePatterns` in `next.config.ts` when pulling images from a CMS or external host — `next/image` will 400 silently.

## Official links

- Docs: https://nextjs.org/docs
- GitHub: https://github.com/vercel/next.js
