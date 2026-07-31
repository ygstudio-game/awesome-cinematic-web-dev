# Lighthouse & the "stays smooth" mindset

**Why Apple-style sites stay smooth despite heavy visuals:** They budget performance *before* adding an effect, not after. Every animation/3D/video element earns its place against a fixed budget (usually: one active WebGL context, a capped total video/image payload for the initial viewport, and 60fps as the hard floor for anything that runs continuously).

## Running an audit

```bash
npm install -g lighthouse
npm run build && npm run start
lighthouse http://localhost:3000 --view --preset=desktop
lighthouse http://localhost:3000 --view   # mobile preset, default
```

Or Chrome DevTools → Lighthouse tab, always audit **mobile** first — it's the stricter constraint and where cinematic sites most often fail.

## Target scores for this stack

| Site type | Performance target |
|---|---|
| Marketing site, no 3D on critical path | 95+ |
| Marketing/product site with hero 3D | 85-95 |
| Heavy scrollytelling/3D flagship page | 75-90 (acceptable if UX genuinely requires it — but still budget deliberately) |

## The five levers, in priority order

1. **Defer everything not needed for first paint** — see `08-Optimization/LazyLoading.md`. This is the single biggest lever; a hero 3D scene loaded via `next/dynamic` after LCP text renders costs almost nothing to Lighthouse's initial metrics.
2. **Cap and compress video/images** — see `Video.md` / `Images.md`.
3. **One active WebGL canvas** — each context has fixed overhead; multiples compound.
4. **Cap device pixel ratio** (`dpr={[1,2]}` in R3F) — rendering at native DPR on a 3x-density phone is 9x the pixel work for no visible gain.
5. **Respect `prefers-reduced-motion`** — not just an accessibility nicety; it's also your built-in low-power fallback path for constrained devices/connections if you additionally gate it behind `navigator.connection.saveData` or similar signals.

## Common mistakes

- Auditing only on desktop — mobile Lighthouse is stricter and closer to real user conditions; always check both.
- Treating a single high score as done — re-audit after adding any new hero-level effect; regressions creep in one component at a time.
- Optimizing bundle size while ignoring main-thread work from continuous `useFrame`/scroll-listener code — Lighthouse's Total Blocking Time and long-task metrics catch this even when the JS bundle itself is small.

## Official links

- https://developer.chrome.com/docs/lighthouse
