---
name: cinematic-web-dev
description: Use when building a cinematic, high-performance marketing/product/portfolio/agency website (Apple/Linear/Stripe-quality bar) with an AI coding agent. Loads the awesome-cinematic-web-dev handbook's stack, hard performance/motion constraints, ready-to-use prompts, and task-to-file routing so the build stays consistent and premium instead of regressing to generic AI-default UI.
---

# Cinematic Web Dev

This skill packages the **awesome-cinematic-web-dev** handbook — a reference library for building Apple/Linear/Stripe-quality cinematic websites (motion-rich, 3D-capable, scroll-driven storytelling) that still score well on Lighthouse.

## When this applies

The user asks for a landing page, product showcase, portfolio, agency site, or SaaS marketing site with any emphasis on: premium/cinematic feel, scroll animation, 3D, video/scrollytelling, or matching a named reference (Apple, Linear, Stripe, Framer). If they just want a plain functional page with no visual ambition, this skill is unnecessary overhead — skip it.

## Procedure

1. **Read `references/AGENTS.md` first.** It is the compact manifest: hard constraints, default stack, and a task→file lookup table into the rest of `references/`. Do not guess stack choices or install commands from memory — look them up there.
2. **Determine site type** and pull the matching ready-to-use prompt from `references/09-Prompts/` (AppleStyle, SaaS, LandingPage, Portfolio, Agency) — use it as-is or adapt it, but keep its structure (exact reference, exact stack, explicit exclusions, architecture expectations). Pattern explained in `references/02-AI/Prompts.md`.
3. **Write a project conventions file** (`CLAUDE.md` or equivalent) in the target project before generating any code, using the hard constraints from `references/AGENTS.md`.
4. **Scaffold** per `references/10-Templates/FolderStructure.md`.
5. **Connect MCP** (Playwright + shadcn at minimum) per `references/03-MCP/` so you can verify sections visually as you build, not just generate code blind.
6. **Build one section at a time** — hero, then next section, verifying each in the browser before continuing. Pull component sources from `references/04-UI/`, animation patterns from `references/05-Animation/`, 3D from `references/06-3D/`, scroll storytelling from `references/07-Storytelling/` (including `ScrollWorld.md` if the user wants a fully AI-generated scroll-scrubbed world flythrough rather than hand-built assets).
7. **Re-check performance** (`references/08-Optimization/Lighthouse.md`) after every new heavy section — 3D, video, or animation-dense component.
8. **Deploy** per `references/11-Deployment/` once approved.

## Hard constraints (non-negotiable, apply regardless of how the user phrased the request)

- One active `<canvas>` (WebGL context) on screen at a time.
- Preload only the next section's assets, never the whole page's up front.
- Every animated component respects `prefers-reduced-motion` with a real fallback.
- Video (MP4/WebM) over GIF, always.
- No GSAP unless Motion.dev genuinely cannot achieve the effect.
- No Spline unless the project needs non-developer scene editing.
- Cap R3F `dpr` to `[1, 2]`.
- Lighthouse mobile target: 90+ with heavy 3D, 95+ without.
- Prefer existing components from `references/04-UI/` over hand-rolled UI.

Full detail and rationale for each: `references/AGENTS.md` and `references/08-Optimization/`.

## Reference contents

```
references/
├── AGENTS.md              manifest — read this first
├── Resources.md            every official link
├── 01-Setup/                Next.js, Tailwind, Motion.dev, R3F, Theatre.js, Lenis, GSAP
├── 02-AI/                    Claude Code, Antigravity, Cursor, Windsurf, Codex, skills, prompt discipline
├── 03-MCP/                   Playwright, MagicUI, shadcn, ReactBits MCP servers
├── 04-UI/                     MagicUI, ReactBits, Aceternity, 21st.dev
├── 05-Animation/               Motion.dev patterns, Motion Primitives, Theatre.js
├── 06-3D/                       React Three Fiber, Drei, Spline, Blender pipeline, WebGPU
├── 07-Storytelling/               Scrollama, ScrollyVideo.js, Basement patterns, scroll-world
├── 08-Optimization/                 Lighthouse, lazy loading, video, images
├── 09-Prompts/                       ready-to-use prompts per site type
├── 10-Templates/                      folder structure + Hero/Pricing/Contact code
└── 11-Deployment/                      Vercel, Cloudflare
```

## Notes

- This is a reference/routing skill, not a code generator by itself — it tells you (the agent) which file has the install command, code pattern, or prompt you need, and which constraints apply. Actually building the site still means writing real project code guided by what's in `references/`.
- Full narrative documentation with human-facing explanations lives in the same repo's `README.md` (not bundled here) if the user wants to read it directly rather than have you act on it.
