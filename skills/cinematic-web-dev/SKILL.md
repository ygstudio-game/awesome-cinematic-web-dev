---
name: cinematic-web-dev
description: Use when building a cinematic, high-performance marketing/product/portfolio/agency/luxury-boutique website (Apple/Linear/Stripe/Cartier quality bar) with an AI coding agent, or when a build-in-progress shows generic AI-template UI, raw Three.js primitive geometry, SaaS pill badges, greedy multi-section scaffolding, or scroll-bound `<video>` stutter.
---

# Cinematic Web Dev

This skill packages the **awesome-cinematic-web-dev** handbook — a reference library for building Apple/Linear/Stripe/luxury-boutique-quality cinematic websites (motion-rich, 3D-capable, scroll-driven storytelling) that still score well on Lighthouse.

## When this applies

The user asks for a landing page, product showcase, portfolio, agency site, luxury boutique, or SaaS marketing site with any emphasis on: premium/cinematic feel, scroll animation, 3D, video/scrollytelling, or matching a named reference (Apple, Linear, Stripe, Framer, Cartier). If they just want a plain functional page with no visual ambition, this skill is unnecessary overhead — skip it.

## Procedure: 4 Mandatory Gatekeeping Checkpoints

AI coding agents default to **Greedy Completion Bias** — generating 8+ complete sections in one turn, which produces shallow filler UI nobody reviewed. Full protocol, diagram, and anti-patterns: `references/HARD_CHECKPOINTS.md`. The four checkpoints are mandatory and run in order — do not skip or collapse them, even under time pressure or a user request to "just build the whole thing."

### Checkpoint 1 — Brand Strategy & User Brainstorming — 🛑 HARD STOP
Read `references/AGENTS.md` first (compact manifest: hard constraints, default stack, task→file lookup). If the user has no brand/creative direction yet, run `references/12-AI-Cinematic-Pipeline/` (Brand Analysis → Creative Brief → Storyboard) to produce one. Present the Brand Concept, Palette, and Storyboard sequence to the user and ask "Does this creative direction match your vision?"
**Do not write any project code until the user approves Checkpoint 1.**

### Checkpoint 2 — Environment & MCP Handshake
Connect all four component/browser MCP servers before generating code blind — do not skip any as "not needed yet":
- `claude mcp add playwright -- npx @playwright/mcp@latest` — see `references/03-MCP/Playwright.md`
- `claude mcp add shadcn -- npx shadcn@latest mcp` — see `references/03-MCP/Shadcn.md` (also fronts MagicUI/Aceternity/21st.dev registries)
- `claude mcp add magicui -- npx @magicui/mcp@latest` — see `references/03-MCP/MagicUI.md`
- `claude mcp add reactbits -- npx reactbits-mcp@latest` — see `references/03-MCP/ReactBits.md`

Then install/enable the design-taste skill(s) from the **Companion Design/Taste Skills** section below — run them before generating the first section, not after. Pull the matching ready-to-use prompt from `references/09-Prompts/` (AppleStyle, SaaS, LandingPage, Portfolio, Agency) — pattern explained in `references/02-AI/Prompts.md`. Write a project conventions file (`CLAUDE.md` or equivalent) using the hard constraints from `references/AGENTS.md`. Scaffold per `references/10-Templates/FolderStructure.md`.

### Checkpoint 3 — Hero Section Only + User Review — 🛑 HARD STOP
Build **only** the Hero section — nothing else. Pull component sources from `references/04-UI/`, animation patterns from `references/05-Animation/`, 3D from `references/06-3D/`, frame-sequence hero from `references/FRAME_SEQUENCE_PIPELINE.md` or `references/12-AI-Cinematic-Pipeline/10-Canvas-Animation.md`. Verify visually with Playwright/browser screenshot, apply the Aesthetic & Craftsmanship Constraints below, then present the screenshot and ask "How is the visual quality, typography, and motion performance of this Hero section?"
**Do not generate section 2 until the user approves Checkpoint 3.**

### Checkpoint 4 — Incremental Section-by-Section Lock
Build subsequent sections **one at a time**, verifying each in the browser and getting user approval before starting the next. Never scaffold 5+ generic filler sections in a single turn. Re-check performance (`references/08-Optimization/Lighthouse.md`) after every heavy section (3D, video, animation-dense). Deploy per `references/11-Deployment/` only once the user has approved the final section.

## Hard constraints (non-negotiable, apply regardless of how the user phrased the request)

- One active `<canvas>` (WebGL context) on screen at a time.
- Preload only the next section's assets, never the whole page's up front.
- Every animated component respects `prefers-reduced-motion` with a real fallback.
- Pre-extracted WebP frame sequence on `<canvas>` over binding scroll to `HTMLVideoElement.currentTime` — see `references/FRAME_SEQUENCE_PIPELINE.md`. Video (MP4/WebM) over GIF elsewhere, always.
- Never place `overflow-x-hidden` (or `overflow-hidden`) on a parent of a `position: sticky` scrollytelling section — sticky silently breaks.
- No GSAP unless Motion.dev genuinely cannot achieve the effect.
- No Spline unless the project needs non-developer scene editing.
- Cap R3F `dpr` to `[1, 2]`.
- Lighthouse mobile target: 90+ with heavy 3D, 95+ without.
- Prefer existing components from `references/04-UI/` over hand-rolled UI.
- Windows dev servers: exclude binary media from Vite HMR watching (`watch: { ignored: ['**/*.mp4', '**/sequence/**'] }`) to avoid `EBUSY` file-lock errors.

Full detail and rationale for each: `references/AGENTS.md` and `references/08-Optimization/`.

## Aesthetic & Craftsmanship Constraints

Technical compliance (Lighthouse 90+, one canvas context) does not prevent the "AI template look" — generic pill badges, centered text over a background video, identical card grids. Full typography scale, color tokens, and layout diagrams: `references/EDITORIAL_DESIGN_SYSTEM.md`.

**Banned by default:**
- Raw, untextured Three.js primitives (`TorusGeometry`, `OctahedronGeometry`, `BoxGeometry`) standing in as the product/hero visual. Use photorealistic GLTF/GLB models, GLSL shaders, HDRI lighting, or a WebP frame sequence instead.
- Generic SaaS pill badges (rounded blue/purple chips with an icon, e.g. "AI Powered", "New Feature").
- Heavy box-shadows or neon glow borders. Use subtle lighting gradients and 1px rule lines instead.
- Crowded, identical 3-card grids as the default layout for feature/showcase sections.

**Required by default:**
- Asymmetrical, pinned split-screen layouts for storytelling/showcase sections (pinned media/canvas on one side, editorial copy with metadata tags on the other) — see the layout diagram in `references/EDITORIAL_DESIGN_SYSTEM.md`.
- Editorial typography contrast: large serif display titles (`72px`-`120px` desktop) against `10px`-`11px` uppercase tracked-out metadata/mono labels — not a uniform sans-serif scale.
- Generous, unhurried whitespace (`px-8 lg:px-20`, `py-16 lg:py-32`) over crowded density.

## Companion Design/Taste Skills (install at Checkpoint 2, before any section is generated)

This skill routes stack/code/checkpoints; it does not by itself fix generic AI design taste. Full category breakdown: `references/02-AI/Skills.md`. Five categories, chain in this order — process/checkpoint skill (this one) → taste skill → implementation:

| Category | Purpose | Install |
|---|---|---|
| Taste / design judgment | Biases layout, spacing, color away from generic AI-default UI | A taste-defining Claude Code skill such as `impeccable`, `design-taste-frontend`, or `high-end-visual-design` — check what's actually installed with your skill listing before naming one; use only **one** at a time (stacking causes conflicting direction) |
| UX rigor / design-system generation | Accessibility, focus states, touch targets, coherent style/color/type system committed up front | UI/UX Pro Max — `references/02-AI/UIUXProMax.md` (`/plugin install ui-ux-pro-max@ui-ux-pro-max-skill` or `npx ui-ux-pro-max-cli init --ai claude`) |
| Responsive craft | Mobile-first by construction, not scaled down from desktop | Bundled into the taste/UX-rigor skill in most toolchains — verify it's covered, don't assume |
| Web quality / performance discipline | Applies the Lighthouse-mindset constraints (`references/08-Optimization/`) during generation, not after | This skill's own Hard Constraints above — always active, no separate install |
| Domain-specific style (optional) | Matches one named designer/aesthetic voice (e.g. an "Emil Kowalski"-style skill) | Only when the user wants that exact voice — e.g. `emil-design-eng` — never combine with a general taste skill in the same build |

Run the taste/UX-rigor skill once, early, so it commits to one style/color/type system before Checkpoint 3's Hero build — re-deriving choices per section is the same inconsistency this category exists to prevent.

## Red Flags — STOP and Reset

If any of these are true, stop generating code and go back to the relevant checkpoint or constraint:

| Red flag | Reset to |
|---|---|
| About to generate 3+ full sections in one turn | Checkpoint 4 — one section at a time |
| Skipping straight to coding with no brand/creative direction confirmed | Checkpoint 1 — hard stop for brainstorming |
| Reaching for `TorusGeometry`/`OctahedronGeometry`/`BoxGeometry` as the hero visual | Aesthetic Constraints — use GLTF/shader/HDRI/frame sequence |
| Binding scroll position to `video.currentTime` on a raw `<video>` | `references/FRAME_SEQUENCE_PIPELINE.md` — extract WebP frames, scrub on canvas |
| A sticky scrollytelling section not sticking | Check for `overflow-x-hidden`/`overflow-hidden` on any parent container |
| Output leans on pill badges, centered-text-over-video hero, or identical card grids | Aesthetic Constraints — banned list |
| Running `cinematic-web-dev` without ever invoking brainstorming/writing-plans or checking Playwright MCP | Checkpoint 1/2 — sub-skill and MCP handshake is mandatory, not optional |
| Generating UI without connecting shadcn/MagicUI/ReactBits MCP, or without a taste/UX-rigor skill installed | Checkpoint 2 — Companion Design/Taste Skills section |
| Windows dev server throwing `EBUSY` on `.mp4`/`public/sequence/**` | Exclude binary media from Vite HMR watch (see Hard constraints) |

**All of these mean: stop, do not keep building on top of the flaw, return to the checkpoint or constraint listed above.**

## Reference contents

```
references/
├── AGENTS.md                        manifest — read this first
├── Resources.md                     every official link
├── HARD_CHECKPOINTS.md              4 mandatory gatekeeping checkpoints protocol
├── EDITORIAL_DESIGN_SYSTEM.md       high-luxury typography, color tokens, layout, banned UI
├── FRAME_SEQUENCE_PIPELINE.md       OpenCV WebP frame extraction + HTML5 canvas scrub engine
├── SKILL_IMPROVEMENTS.md            audit of 7 real-world failure modes and their remedies
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
├── 11-Deployment/                      Vercel, Cloudflare
└── 12-AI-Cinematic-Pipeline/            idea → brand analysis → creative brief → storyboard →
                                          AI image/video prompts → generated media → optimized
                                          frame sequence → website generation → deployment
```

## Notes

- This is a reference/routing skill, not a code generator by itself — it tells you (the agent) which file has the install command, code pattern, checkpoint, or constraint you need. Actually building the site still means writing real project code guided by what's in `references/`.
- `references/SKILL_IMPROVEMENTS.md` is the source audit (VELORIA project) that the checkpoints and aesthetic constraints above were extracted from — read it if a failure mode isn't covered above and you need the original context.
- Full narrative documentation with human-facing explanations lives in the same repo's `README.md` (not bundled here) if the user wants to read it directly rather than have you act on it.
