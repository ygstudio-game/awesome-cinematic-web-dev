# AGENTS.md

Machine-readable manifest for this repo. Load this file first. It is the index — follow the file pointers for implementation detail instead of guessing from memory. `README.md` is the human-facing version of this same content; skip it unless the user asks you to explain the repo to them.

## What this repo is

A reference/prompt library for building cinematic, high-performance marketing/product websites (Apple/Linear/Stripe-quality bar). Use it when a user asks you to build a landing page, product showcase, portfolio, agency site, or SaaS marketing site with an emphasis on motion, 3D, or scroll storytelling.

If the user is starting from a bare idea (no brand assets, no design direction yet) and wants AI to drive brand/creative decisions end-to-end, use `12-AI-Cinematic-Pipeline/` instead of jumping straight to `09-Prompts/` — it produces a Creative Brief that keeps every later step (storyboard, prompts, generated media, and the final site) consistent with a single creative vision. See that module's `README.md` for the full idea-to-deployment workflow.

## Hard constraints — apply to every build regardless of prompt wording

- One active `<canvas>` (WebGL context) on screen at a time.
- Preload only the next section's assets, never the whole page's up front.
- Every animated component must respect `prefers-reduced-motion` with a real fallback (not just disabled motion + layout jank).
- Video over GIF: MP4/WebM only.
- No GSAP unless Motion.dev cannot achieve the effect — check `01-Setup/GSAP.md` before adding it.
- No Spline unless the project needs non-developer scene editing — check `06-3D/Spline.md` before adding it.
- Cap R3F `dpr` to `[1, 2]`.
- Lighthouse mobile target: 90+ with heavy 3D, 95+ without. Re-check after every new heavy section, not just at the end (`08-Optimization/Lighthouse.md`).
- Prefer existing components from `04-UI/` (MagicUI/ReactBits/Aceternity/21st.dev) over hand-rolled UI.

## Default stack

Next.js (App Router) → Tailwind v4 → Motion.dev → Lenis → React Three Fiber + Drei → Theatre.js → ScrollyVideo.js + Scrollama → MagicUI/ReactBits/21st.dev → Playwright/shadcn/MagicUI MCP.

Full install commands: `01-Setup/*.md` (one file per library — NextJS, Tailwind, Motion, R3F, Theatre, Lenis, GSAP).

## Task → file map

| If the task involves | Load |
|---|---|
| Initial project scaffold | `01-Setup/NextJS.md`, `10-Templates/FolderStructure.md` |
| A specific library's install/API | `01-Setup/<Library>.md` |
| Choosing which AI tool/workflow to run as | `02-AI/<Tool>.md` (Claude, Antigravity, Cursor, Windsurf, Codex) |
| Writing a generation prompt | `02-AI/Prompts.md` (pattern) or `09-Prompts/<SiteType>.md` (ready-to-use) |
| Connecting MCP servers | `03-MCP/Playwright.md`, `03-MCP/Shadcn.md`, `03-MCP/MagicUI.md`, `03-MCP/ReactBits.md` |
| Sourcing a UI component | `04-UI/<Kit>.md` — check before hand-writing one |
| Page transitions, reveals, micro-interactions | `05-Animation/Motion.md` |
| 3D sequencing / camera timelines | `05-Animation/Theatre.md` |
| A 3D scene, product showcase, hero object | `06-3D/R3F.md`, `06-3D/Drei.md` |
| 3D source assets from Blender | `06-3D/Blender.md` |
| Non-dev-editable marketing 3D scene | `06-3D/Spline.md` |
| Step-based scroll narrative | `07-Storytelling/Scrollama.md` |
| Scroll-scrubbed video sequence | `07-Storytelling/ScrollyVideo.md` |
| Live-WebGL continuous scroll scene | `07-Storytelling/Basement.md` |
| Fully AI-generated scroll world flythrough (no hand-authored assets) | `07-Storytelling/ScrollWorld.md` |
| Lighthouse / general performance | `08-Optimization/Lighthouse.md` |
| Deferring assets/components | `08-Optimization/LazyLoading.md` |
| Video encoding | `08-Optimization/Video.md` |
| Image optimization | `08-Optimization/Images.md` |
| Hero / Pricing / Contact section code | `10-Templates/<Section>.md` |
| Deployment | `11-Deployment/Vercel.md` or `11-Deployment/Cloudflare.md` |
| Any official link/version check | `Resources.md` |
| Building from a bare idea (brand/creative decisions not yet made) | `12-AI-Cinematic-Pipeline/README.md` — start there instead of `09-Prompts/` |
| Analyzing a brand from a raw idea | `12-AI-Cinematic-Pipeline/02-Brand-Analysis.md` |
| Producing the project's single source-of-truth creative direction | `12-AI-Cinematic-Pipeline/03-Creative-Director.md` |
| Generating a scene-by-scene storyboard | `12-AI-Cinematic-Pipeline/04-Storytelling.md` |
| Writing AI image/video generation prompts | `12-AI-Cinematic-Pipeline/05-Prompt-Generation.md` |
| Sourcing AI-generated stills or video clips | `12-AI-Cinematic-Pipeline/06-Image-Generation.md`, `12-AI-Cinematic-Pipeline/07-Video-Generation.md` |
| Compressing/converting a generated video clip | `12-AI-Cinematic-Pipeline/08-Video-Optimization.md` |
| Extracting a frame sequence + manifest from video | `12-AI-Cinematic-Pipeline/09-Frame-Extraction.md` |
| Rendering a scroll-scrubbed canvas frame sequence | `12-AI-Cinematic-Pipeline/10-Canvas-Animation.md` |
| Generating the full site from a completed Creative Brief | `12-AI-Cinematic-Pipeline/11-Website-Generation.md` |

## Build procedure

**If the user already has brand direction / just wants a coded site:**

1. Confirm/write a project `CLAUDE.md` (or equivalent) with the hard constraints above plus the chosen stack — do this before generating any code.
2. Scaffold per `10-Templates/FolderStructure.md`.
3. Connect Playwright MCP + shadcn MCP before building UI (`03-MCP/`).
4. Build one section at a time: generate → open in browser via MCP → verify → next section. Do not generate the whole page in one pass.
5. After adding any 3D/video/heavy-animation section, re-run a Lighthouse check.
6. Deploy per `11-Deployment/`.

**If the user is starting from a bare idea:** run `12-AI-Cinematic-Pipeline/` first (Brand Analysis → Creative Brief → Storyboard → prompts → generated media → optimization → frame extraction), then proceed through steps 1-6 above using `12-AI-Cinematic-Pipeline/11-Website-Generation.md` in place of a `09-Prompts/` prompt — it consumes the Creative Brief the pipeline produced instead of a bare site-type description.

## Prompt-writing rule

Generic asks ("make it premium") regress to generic output. Always specify: exact reference site/brand tier, exact stack, explicit exclusions (what NOT to use/do), and architecture expectations (typed props, shared timing constants, composable subcomponents). Ready-made versions of this: `09-Prompts/*.md`.

## Drift risk

Install commands/package names for smaller or newer tools may be stale — verify against the linked official source before running, especially for: `03-MCP/*.md`, `05-Animation/ReactKino.md`, `07-Storytelling/ScrollWorld.md`. Core libraries (Next.js, Tailwind, Three.js, Motion.dev) are stable and lower risk.
