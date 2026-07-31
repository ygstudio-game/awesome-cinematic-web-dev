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

- [Install as a skill (recommended)](#install-as-a-skill-recommended)
- [Who this is for](#who-this-is-for)
- [Repo structure](#repo-structure)
- [Quick start — tell your agent to build this](#quick-start--tell-your-agent-to-build-this)
- [Which AI tool should you use](#which-ai-tool-should-you-use)
- [How to actually use this repo](#how-to-actually-use-this-repo)
- [Getting the best output from your AI agent](#getting-the-best-output-from-your-ai-agent)
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
npx skills add <your-github-username>/awesome-cinematic-web-dev
npx skills add <your-github-username>/awesome-cinematic-web-dev -a codex   # target Codex directly
```

**Manually (drop-in skill):**

```bash
git clone https://github.com/<your-github-username>/awesome-cinematic-web-dev
cp -R awesome-cinematic-web-dev/skills/cinematic-web-dev ~/.claude/skills/   # Claude Code
cp -R awesome-cinematic-web-dev/skills/cinematic-web-dev ~/.codex/skills/    # Codex
```

Once installed, just ask your agent for a cinematic landing page/product page/portfolio — it'll pick up the skill automatically (or invoke it explicitly, e.g. `/cinematic-web-dev` in Claude Code).

> The `npx skills add` and `git clone` commands above assume this repo has been pushed to your own GitHub account — replace `<your-github-username>/awesome-cinematic-web-dev` with wherever you've published it. Until then, use the manual copy method by pointing `cp -R` at this local folder directly: `cp -R skills/cinematic-web-dev ~/.claude/skills/`.

## Who this is for

You want a marketing site, product page, portfolio, or agency site that feels like Apple/Linear/Stripe — and you're using an AI agent to actually build it, not hand-writing every component yourself. You don't need to be a developer to use this repo: your job is to point your agent at the right file, hand it the right prompt, and check what comes back. This repo exists because "make it look premium" alone produces generic output every time — the difference between that and a genuinely great result is *what you tell the agent, and in what order.*

## Repo structure

```
awesome-cinematic-web-dev/
├── README.md              you are here
├── Resources.md            every official link in one place + inspiration sources
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
└── 11-Deployment/                      how your agent ships the finished site
```

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

1. **Read `08-Optimization/Lighthouse.md`** — even briefly — before you start, so you know what "fast" means here and can bake it into your first instruction rather than fixing it after the site looks good and scores 40.
2. **Tell your agent which stack to use** — [the default below](#the-recommended-default-stack) is right for most projects; point your agent at `01-Setup/` if it needs install details for any piece.
3. **Have it scaffold using `10-Templates/FolderStructure.md`** so components, 3D scenes, and storytelling code land in predictable places instead of wherever the agent decides that session.
4. **Give it a project conventions file** (`CLAUDE.md`, `.cursorrules`, or equivalent) — see [Getting the best output](#getting-the-best-output-from-your-ai-agent). This is the single highest-leverage thing you can hand your agent.
5. **Build one section at a time**, handing it prompts from `09-Prompts/` and pointing it at `04-UI/`, `05-Animation/`, `06-3D/`, `07-Storytelling/` for the pieces each section needs.
6. **Have it show you its work in the browser**, not just describe the code — set up MCP (`03-MCP/`) so it can actually check.
7. **Ask for a Lighthouse check** after every new heavy section (video, 3D, big animation) — not just once at the end.
8. **Have it deploy** per `11-Deployment/` once you're happy.

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

Don't ask for the whole site in one message. A bad structural call in the hero compounds through every section generated to match it — catching it immediately is far cheaper than catching it at the end.

### 4. Make sure your agent can actually see what it built

This is what MCP is for (`03-MCP/`). Without it, your agent only ever reads its own source code — it can write a scroll animation that's syntactically fine but visually broken (wrong timing, overlapping elements, a 3D scene that never renders) with no way to notice. Connect Playwright MCP and explicitly ask it to open the page and check.

### 5. Let it pull real components instead of guessing at them

MagicUI MCP, shadcn MCP, and ReactBits MCP (`03-MCP/`) give your agent live access to actual, current component code. Without them, asking for "an animated marquee" gets you a plausible-looking but unmaintained approximation instead of the real, tested component.

### 6. If your tool supports skills, load taste/UX ones before generating

Claude Skills or equivalent custom rule sets (`02-AI/Skills.md`) bias the *first draft* toward good design decisions — cheaper than asking your agent to fix a mediocre one afterward.

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
- MP4/WebM over GIF, always.
- Target Lighthouse 90+ on mobile for a site with heavy 3D; 95+ if there's no 3D on the critical path.

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
