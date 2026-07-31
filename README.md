# Awesome Cinematic Web Dev

A handbook + prompt/component library for directing an **AI coding agent** — Claude Code, Antigravity, Cursor, Windsurf, or Codex — to build an Apple / Linear / Stripe / Framer-quality website for you: cinematic, motion-rich, 3D-capable, and **still fast**.

This repo isn't code you write by hand. It's the reference material and ready-to-use prompts you hand to your agent so it builds something with real taste and performance discipline, instead of the generic AI-default template (centered hero, three feature cards, gradient blob) every agent produces when just asked to "make it look premium."

> **If you're an AI agent reading this repo:** read [`AGENTS.md`](AGENTS.md) instead of this file — it's the compact, machine-first index with hard constraints and a task→file lookup table. This README is the narrative version for the human directing you.

```
Next.js → Tailwind → Motion.dev → Lenis → React Three Fiber + Drei → Theatre.js
   → ScrollyVideo.js + Scrollama → MagicUI + ReactBits + 21st.dev → Playwright/shadcn/MagicUI MCP
```

---

## Table of contents

- [Awesome Cinematic Web Dev](#awesome-cinematic-web-dev)
  - [Table of contents](#table-of-contents)
  - [Install as a skill (recommended)](#install-as-a-skill-recommended)
  - [Who this is for](#who-this-is-for)
  - [Repo structure](#repo-structure)
  - [The AI Cinematic Pipeline — from bare idea to deployed site](#the-ai-cinematic-pipeline--from-bare-idea-to-deployed-site)
  - [Quick start — tell your agent to build this](#quick-start--tell-your-agent-to-build-this)
  - [Which AI tool should you use](#which-ai-tool-should-you-use)
  - [How to actually use this repo](#how-to-actually-use-this-repo)
  - [Getting the best output from your AI agent](#getting-the-best-output-from-your-ai-agent)
    - [1. Give it a conventions file before the first prompt](#1-give-it-a-conventions-file-before-the-first-prompt)
    - [2. Name the exact reference — and name what to avoid](#2-name-the-exact-reference--and-name-what-to-avoid)
    - [3. Ask for one section at a time, and look at each before continuing](#3-ask-for-one-section-at-a-time-and-look-at-each-before-continuing)
    - [4. Make sure your agent can actually see what it built](#4-make-sure-your-agent-can-actually-see-what-it-built)
    - [5. Let it pull real components instead of guessing at them](#5-let-it-pull-real-components-instead-of-guessing-at-them)
    - [6. If your tool supports skills, load taste/UX ones before generating](#6-if-your-tool-supports-skills-load-tasteux-ones-before-generating)
    - [7. Re-check performance after every new heavy section](#7-re-check-performance-after-every-new-heavy-section)
  - [Choosing a stack by project type](#choosing-a-stack-by-project-type)
  - [The recommended default stack](#the-recommended-default-stack)
  - [Non-negotiable performance rules](#non-negotiable-performance-rules)
  - [Recommended build order](#recommended-build-order)
  - [Troubleshooting / FAQ](#troubleshooting--faq)
  - [Keeping this handbook current](#keeping-this-handbook-current)

---

## Install as a skill (recommended)

The whole handbook is also packaged as a `SKILL.md`-compatible skill at [`skills/cinematic-web-dev/`](skills/cinematic-web-dev/) — install it once and any SKILL.md-compatible agent (Claude Code, Codex, and others) can load the manifest, constraints, and every reference file on demand, instead of you manually pointing it at files in this repo each session.

**Via Vercel's cross-agent skills CLI** (installs into Claude Code, Codex, Cursor, and 20+ other agents):

```bash
npx skills add ygstudio-game/awesome-cinematic-web-dev
npx skills add ygstudio-game/awesome-cinematic-web-dev -a codex   # target Codex directly
```

**Manually (drop-in skill):**

```bash
git clone https://github.com/ygstudio-game/awesome-cinematic-web-dev
cp -R awesome-cinematic-web-dev/skills/cinematic-web-dev ~/.claude/skills/   # Claude Code
cp -R awesome-cinematic-web-dev/skills/cinematic-web-dev ~/.codex/skills/    # Codex
```

Once installed, just ask your agent for a cinematic landing page/product page/portfolio — it'll pick up the skill automatically (or invoke it explicitly, e.g. `/cinematic-web-dev` in Claude Code).

> The `npx skills add` and `git clone` commands above assume this repo has been pushed to your own GitHub account — replace `ygstudio-game/awesome-cinematic-web-dev` with wherever you've published it. Until then, use the manual copy method by pointing `cp -R` at this local folder directly: `cp -R skills/cinematic-web-dev ~/.claude/skills/`.

## Who this is for

You want a marketing site, product page, portfolio, or agency site that feels like Apple/Linear/Stripe — and you're using an AI agent to actually build it, not hand-writing every component yourself. You don't need to be a developer to use this repo: your job is to point your agent at the right file, hand it the right prompt, and check what comes back. This repo exists because "make it look premium" alone produces generic output every time — the difference between that and a genuinely great result is *what you tell the agent, and in what order.*

## Repo structure

```
awesome-cinematic-web-dev/
├── README.md              you are here
├── Resources.md            every official link in one place + inspiration sources
├── HARD_CHECKPOINTS.md     4 mandatory gatekeeping checkpoints (brand approval, hero-only review) — read before building
├── EDITORIAL_DESIGN_SYSTEM.md  typography, color tokens, layout, and the "AI template look" banned-UI list
├── FRAME_SEQUENCE_PIPELINE.md  OpenCV WebP frame extraction + HTML5 canvas scroll-scrub engine
├── SKILL_IMPROVEMENTS.md   audit of real-world failure modes these files were hardened against
│
├── 01-Setup/                what your agent installs/configures for each core library
├── 02-AI/                    Claude Code / Antigravity / Cursor / Windsurf / Codex — how to direct each one
├── 03-MCP/                   lets your agent see and test the actual running site, not just its own code
├── 04-UI/                     component kits to point your agent at (MagicUI / ReactBits / Aceternity / 21st.dev)
├── 05-Animation/               motion patterns to hand your agent (Motion.dev, Theatre.js)
├── 06-3D/                       3D scene patterns (React Three Fiber, Drei, Spline, Blender pipeline)
├── 07-Storytelling/               scroll-driven storytelling, including a skill that AI-generates a whole scene
├── 08-Optimization/                 the performance rules to bake into every instruction you give your agent
├── 09-Prompts/                       full, ready-to-paste prompts per site type — start here if you're in a hurry
├── 10-Templates/                      reference code your agent can be pointed at or asked to match
├── 11-Deployment/                      how your agent ships the finished site
└── 12-AI-Cinematic-Pipeline/            idea → brand analysis → creative brief → storyboard → AI-generated
                                          media → website — for starting from a bare idea, not just a prompt
```

## The AI Cinematic Pipeline — from bare idea to deployed site

Everything above assumes you already know roughly what the site should look like and just need a prompt to hand your agent. If you're starting from nothing but an idea — no brand direction, no visual concept yet — use [`12-AI-Cinematic-Pipeline/`](12-AI-Cinematic-Pipeline/) instead. It's a full workflow where AI acts as brand strategist and creative director, not just implementer:

```
Idea → Brand Analysis → Creative Brief (single source of truth) → Storyboard
     → Image/Video prompts → Generate media (any provider) → Optimize → Extract frames
     → Generate website → Deploy
```

The key architectural idea: every step reads from one **Creative Brief** instead of each step reinventing the brand on its own — the same reason this handbook has you write a conventions file for coding, applied to creative decisions too. See the module's own [`README.md`](12-AI-Cinematic-Pipeline/README.md) for the full workflow, and [`ROADMAP.md`](12-AI-Cinematic-Pipeline/ROADMAP.md) for why video generation is a manual, provider-agnostic step for now.

Once the pipeline produces a Creative Brief and generated media, its `11-Website-Generation.md` prompt takes over — it's a superset of the prompts in `09-Prompts/` that additionally consumes everything the pipeline produced.

## Quick start — tell your agent to build this

Open Claude Code, Antigravity, Cursor, or your agent of choice in an empty project folder, and give it something like:

```
Set up a Next.js (App Router) + Tailwind project. Install Motion.dev, Lenis,
React Three Fiber, Drei, Theatre.js, ScrollyVideo, and Scrollama.

Then follow the conventions and folder structure in this handbook:
[paste the contents of 02-AI/Claude.md's CLAUDE.md block, and 10-Templates/FolderStructure.md]

Connect Playwright MCP and shadcn MCP so you can see and test the site as you build it
(see 03-MCP/Playwright.md and 03-MCP/Shadcn.md for setup commands).

Once set up, build the hero section using this prompt: [paste from 09-Prompts/].
Show me the result before moving to the next section.
```

Your agent will handle running the actual `npm install` / CLI commands shown throughout `01-Setup/` and `03-MCP/` — those command blocks are there for your agent to execute (or for you to sanity-check what it ran), not something you're expected to type yourself unless you want to.

## Which AI tool should you use

| Tool | Best for | Setup guide |
|---|---|---|
| **Claude Code** | Primary recommendation for this stack — strongest at holding many files (config, components, prompts) consistent across a long build | `02-AI/Claude.md` |
| **Antigravity** | More autonomous, "run for a while and check back" workflows with built-in browser self-verification | `02-AI/Antigravity.md` |
| **Cursor** | Fast, contained inline edits once the main structure exists — great for tweaking one section at a time | `02-AI/Cursor.md` |
| **Windsurf** | Alternative to Cursor with a similar agentic editing loop | `02-AI/Windsurf.md` |
| **Codex** | Solid alternative if your team already has OpenAI tooling in place | `02-AI/Codex.md` |

You don't have to pick just one — many people use Claude Code or Antigravity for the initial multi-section build, then Cursor for quick individual tweaks afterward.

## How to actually use this repo

This repo enforces **4 Mandatory Gatekeeping Checkpoints** (full protocol: [`HARD_CHECKPOINTS.md`](HARD_CHECKPOINTS.md)) so your agent can't skip straight to a pile of unreviewed code — two of them are hard stops where your agent must wait for your explicit approval before continuing:

1. 🛑 **Checkpoint 1 — Brand strategy approval.** If you haven't given brand direction yet, your agent runs `12-AI-Cinematic-Pipeline/` first and presents the concept/palette/storyboard for you to approve. **No project code gets written before this.**
2. **Checkpoint 2 — Environment & MCP handshake.** Connect Playwright, shadcn, MagicUI, and ReactBits MCP (`03-MCP/`), install a taste/UX skill (see point 6 below), write the conventions file, scaffold per `10-Templates/FolderStructure.md`.
3. 🛑 **Checkpoint 3 — Hero-only review.** Your agent builds *only* the Hero section, shows you a screenshot, and waits for your approval before touching section 2.
4. **Checkpoint 4 — One section at a time.** Every remaining section is built, verified in the browser, and approved before the next one starts — never 3+ sections in a single pass. Lighthouse gets re-checked after every heavy section, and deployment (`11-Deployment/`) happens only once the last section is approved.

Read `08-Optimization/Lighthouse.md` before you start so you know what "fast" means here, and see [Getting the best output](#getting-the-best-output-from-your-ai-agent) for how to make each checkpoint actually produce a good result rather than a rubber-stamped one.

## Getting the best output from your AI agent

This is the part that actually separates "one great page, five generic ones" from a consistently premium site.

### 1. Give it a conventions file before the first prompt

Without one, you re-explain your rules every session and the agent drifts. With one, every session inherits them. Hand your agent this (or the fuller version in `02-AI/Claude.md`) to save as `CLAUDE.md`, `.cursorrules`, or its equivalent:

```markdown
# Project conventions

Stack: Next.js App Router, Tailwind v4, Motion.dev, React Three Fiber + Drei, Lenis.
- No GSAP unless Motion.dev genuinely cannot achieve the effect (see 01-Setup/GSAP.md).
- Only one active <canvas> on screen at a time.
- Respect prefers-reduced-motion on every animated component.
- Prefer MagicUI / ReactBits / 21st.dev components over hand-rolled UI — check 04-UI/ first.
- Reference this handbook's 09-Prompts/ and 10-Templates/ before inventing new patterns.
```

### 2. Name the exact reference — and name what to avoid

"Make it cinematic and premium" gets you generic output. "Apple/Linear-quality, no gradient blobs, no centered-hero-with-three-cards" actually shifts what the agent produces. Every prompt in `09-Prompts/` is written this way — use them as-is or as a template for your own asks (pattern explained in `02-AI/Prompts.md`).

### 3. Ask for one section at a time, and look at each before continuing

Don't ask for the whole site in one message — this is enforced, not just advised, via the 4 checkpoints in [`HARD_CHECKPOINTS.md`](HARD_CHECKPOINTS.md). A bad structural call in the hero compounds through every section generated to match it — catching it immediately, at Checkpoint 3, is far cheaper than catching it at the end. If your agent (or the skill package) proposes generating 3+ sections in one pass, that's the "Greedy Completion Bias" failure mode this repo was hardened against — stop it and go back to one section at a time.

### 4. Make sure your agent can actually see what it built

This is what MCP is for (`03-MCP/`). Without it, your agent only ever reads its own source code — it can write a scroll animation that's syntactically fine but visually broken (wrong timing, overlapping elements, a 3D scene that never renders) with no way to notice. Connect Playwright MCP and explicitly ask it to open the page and check.

### 5. Let it pull real components instead of guessing at them

MagicUI MCP, shadcn MCP, and ReactBits MCP (`03-MCP/`) give your agent live access to actual, current component code. Without them, asking for "an animated marquee" gets you a plausible-looking but unmaintained approximation instead of the real, tested component.

### 6. If your tool supports skills, load taste/UX ones before generating

Claude Skills or equivalent custom rule sets (`02-AI/Skills.md`) bias the *first draft* toward good design decisions — cheaper than asking your agent to fix a mediocre one afterward. Concretely, at Checkpoint 2, install:

- **A taste skill** (one at a time — stacking multiple pulls output in conflicting directions), e.g. `impeccable`, `design-taste-frontend`, or `high-end-visual-design` if your tool has them available.
- **UI/UX Pro Max** (`02-AI/UIUXProMax.md`) for a committed style/color/typography system generated once, up front, rather than re-derived per section.
- Optionally a **domain-specific style skill** (e.g. `emil-design-eng`) only when you want that one named designer's voice — don't combine with a general taste skill.

Without one of these, technical compliance (fast, one canvas, respects reduced-motion) still doesn't stop the "AI template look" — generic pill badges, centered-text-over-video heroes, identical 3-card grids. See [`EDITORIAL_DESIGN_SYSTEM.md`](EDITORIAL_DESIGN_SYSTEM.md) for the specific banned patterns and the editorial alternative (asymmetrical split-screens, serif/mono typographic contrast).

### 7. Re-check performance after every new heavy section

One new 3D scene, video, or animation-heavy component can tank your Lighthouse score even if the change "looks small" in the diff. Ask for a check after each one, not just at the end — see `08-Optimization/Lighthouse.md`.

## Choosing a stack by project type

| Site type | Prompt to hand your agent | Notes |
|---|---|---|
| Product showcase (Apple-style) | `09-Prompts/AppleStyle.md` | Live R3F hero, ScrollyVideo fallback on mobile |
| SaaS marketing site | `09-Prompts/SaaS.md` | Skip 3D hero — show the real product instead |
| General landing page | `09-Prompts/LandingPage.md` | Linear/Stripe restraint, MagicUI/21st.dev components |
| Portfolio | `09-Prompts/Portfolio.md` | Editorial/cinematic, ScrollyVideo + text-effect components |
| Agency / flagship brand site | `09-Prompts/Agency.md` | One signature R3F + Theatre.js moment, Scrollama case studies |
| Full AI-generated world flythrough | `07-Storytelling/ScrollWorld.md` | An installable agent skill that generates the 3D art and camera flight for you — no hand-authored assets needed |
| Starting from a bare idea, no brand direction yet | `12-AI-Cinematic-Pipeline/README.md` | AI drives brand analysis, creative direction, and storyboard before any prompt gets written |

## The recommended default stack

```
Next.js (App Router)
  └─ Tailwind CSS
       └─ Motion.dev            → transitions, reveals, micro-interactions
            └─ Lenis            → smooth scroll
                 └─ React Three Fiber + Drei   → 3D
                      └─ Theatre.js            → 3D sequencing/animation timelines
                           └─ ScrollyVideo.js + Scrollama → scrollytelling
                                └─ MagicUI + ReactBits + 21st.dev → UI components
                                     └─ Playwright MCP / shadcn MCP / MagicUI MCP → AI workflow
```

Tell your agent GSAP is opt-in only, for the rare animation Motion.dev genuinely can't do well (`01-Setup/GSAP.md`). Same for Spline — opt-in only, for non-developer-editable marketing scenes (`06-3D/Spline.md`); otherwise it should build 3D directly in React Three Fiber.

## Non-negotiable performance rules

Bake these into your conventions file so your agent never has to be reminded per-prompt:

- One active `<canvas>` (WebGL context) on screen at a time.
- Preload only what the *next* section needs — never the whole page's assets up front.
- Respect `prefers-reduced-motion`; ship a simpler, motion-free fallback, don't just disable animation and leave layout jank.
- Scroll-scrubbed reveals (product/hero) use a pre-extracted WebP frame sequence on `<canvas>`, not `video.currentTime` binding — binding to a raw `<video>` element stutters and drops frames on scroll. See [`FRAME_SEQUENCE_PIPELINE.md`](FRAME_SEQUENCE_PIPELINE.md). MP4/WebM over GIF elsewhere, always.
- Never put `overflow-x-hidden` (or `overflow-hidden`) on a parent of a `position: sticky` scrollytelling section — sticky breaks silently.
- Target Lighthouse 90+ on mobile for a site with heavy 3D; 95+ if there's no 3D on the critical path.
- On Windows, exclude binary media from Vite's HMR watcher (`watch: { ignored: ['**/*.mp4', '**/sequence/**'] }`) or you'll hit `EBUSY` file-lock errors mid-build.

See `08-Optimization/` for the mechanics behind each rule.

## Recommended build order

```
Wireframe / content outline (yours, on paper or in a doc)
    ↓
Write the conventions file and hand it to your agent
    ↓
Have your agent scaffold Next.js + Tailwind (01-Setup/)
    ↓
Have it connect MCP so it can see the running app (03-MCP/)
    ↓
Build hero → check it → next section → check it → ...
    ↓
Point it at MagicUI / ReactBits / 21st.dev for components as needed (04-UI/)
    ↓
Layer in Motion.dev, then Lenis smooth scroll (05-Animation/)
    ↓
Add R3F/Theatre.js or ScrollyVideo/Scrollama storytelling if the project calls for it (06-3D/, 07-Storytelling/)
    ↓
Have it optimize images, video, lazy loading (08-Optimization/)
    ↓
Run a Lighthouse audit — mobile first
    ↓
Have it deploy (11-Deployment/)
```

## Troubleshooting / FAQ

**My agent's output feels generic no matter what I ask for.**
You're likely missing a conventions file and/or not naming explicit exclusions in your prompt. See [Getting the best output](#getting-the-best-output-from-your-ai-agent), points 1 and 2.

**The 3D scene tanks performance on mobile.**
Have your agent check: single canvas, capped `dpr` (`06-3D/R3F.md`), and consider a ScrollyVideo fallback below a breakpoint (`09-Prompts/AppleStyle.md`).

**Scroll-driven animation feels janky.**
Confirm Lenis is actually wired up and other scroll listeners are routed through it rather than raw scroll events — `01-Setup/Lenis.md`.

**Should I let it use GSAP?**
Only if Motion.dev genuinely can't do the effect. Point your agent at `01-Setup/GSAP.md` before it reaches for GSAP by default.

**Claude Code vs. Antigravity vs. Cursor vs. Codex — which one?**
See [Which AI tool should you use](#which-ai-tool-should-you-use) above.

**I don't want to write any prompts myself — can I just ask for the whole thing?**
You can, but you'll get better results asking for one section at a time and checking each — see point 3 in Getting the best output. If you do want a single large ask, use the fully-written prompts in `09-Prompts/` as-is rather than writing your own from scratch.

## Keeping this handbook current

Library APIs, MCP package names, and smaller emerging tools move faster than established ones (Next.js, Tailwind, Three.js). Before your agent relies on an install command or link in this repo for anything beyond the core, well-established libraries, have it check the linked official source — flagged explicitly in files where this is most likely to drift (`03-MCP/`, `05-Animation/ReactKino.md`, `07-Storytelling/ScrollWorld.md`).
