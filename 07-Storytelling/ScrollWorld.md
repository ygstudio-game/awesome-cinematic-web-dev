# scroll-world (AI-generated scroll-scrubbed world flythrough)

**What it is:** An installable Claude Code / Codex skill (`SKILL.md`-compatible, works in any agent supporting that format) that generates an entire immersive "camera flies through a generated world" landing page — the technique behind sites like Emons logistics, where scrolling drives a camera continuously through a sequence of AI-rendered isometric diorama scenes with no cuts between them.

**Why it's different from `ScrollyVideo.md`/`Basement.md`:** Those assume *you* already have footage or a live 3D scene to sync to scroll. scroll-world generates the actual art and camera-flight video clips for you via AI (stills through GPT Image / Higgsfield, camera flights via Seedance/Kling image-to-video), frame-locks the seams between consecutive scenes so the connector clips are frame-identical to their neighbors, then wires the whole chain to a portable vanilla-JS scroll-scrub engine.

**When to use it:** You want a genuine Apple-style scroll-through product/brand experience but don't have (or want to build) custom 3D/video assets by hand — good fit for `09-Prompts/Agency.md`-style flagship hero moments or a whole-page brand story, without hand-authoring in Blender/R3F.

**When to use R3F + Theatre.js instead (`06-3D/`, `05-Animation/Theatre.md`):** You need live interactivity (not just a fixed pre-rendered flight path), want full control over exact geometry/branding rather than AI-generated diorama art, or want zero per-render generation cost.

## Install

As a Claude Code plugin (recommended):

```bash
/plugin marketplace add oso95/scroll-world
/plugin install scroll-world@scroll-world
```

Then ask for a scroll-through world landing page, or invoke `/scroll-world`.

Via Vercel's cross-agent skills CLI (Codex, Cursor, 20+ agents):

```bash
npx skills add oso95/scroll-world
npx skills add oso95/scroll-world -a codex   # target Codex directly
```

Manually (drop into any agent's skills directory):

```bash
git clone https://github.com/oso95/scroll-world
cp -R scroll-world/skills/scroll-world ~/.claude/skills/   # Claude Code
cp -R scroll-world/skills/scroll-world ~/.codex/skills/    # Codex
```

## Requirements

- **Monid CLI** with API key + balance — default video-chain backend (Seedance 2.0, billed per clip; a 6-scene 1080p chain is roughly $27).
- **Higgsfield CLI**, authenticated (`higgsfield auth login`) — renders scene stills and is the fallback for the full chain if Monid is unavailable.
- **ffmpeg / ffprobe** — frame extraction and encoding.
- **Python 3 + Pillow** — mobile portrait canvases, optional transparent-scene knockout.
- **Codex CLI** (optional) — if present, stills can generate through Codex's `image_gen` billed to a ChatGPT subscription instead of Higgsfield credits.

## What it does, concretely

1. **Interviews you** — subject/industry, brand kit (URL import, hand it over, or proposed), art direction, ordered scene list the camera visits, mobile opt-in (native 9:16 portrait chain, not a landscape crop), and budget — shows estimated cost per render tier before generating anything.
2. **Generates assets** — one still per scene, one dive-in camera clip per scene, and connector clips generated from the neighbors' actual rendered frames so every seam is frame-identical (no visible cut/pop between scenes).
3. **Wires it up** — a config-driven scroll engine plays the whole chain as one continuous flight; portrait clips/posters serve automatically on phones.

## Fits into this handbook's stack as

```
Lenis / native scroll position
   → scroll-world's scrub engine (scrub-engine.js — portable, framework-agnostic:
     drops into plain HTML, Next.js, Vue, or a Python-served page)
        → plays the AI-generated flight chain in sync with scroll
```

Since the scrub engine is plain JS with no framework assumption, it can sit alongside the rest of this handbook's Next.js/Tailwind/Motion.dev stack as a self-contained section rather than requiring architectural changes elsewhere on the page.

## Common mistakes

- Treating it as free — asset generation is real spend (~N image gens + ~2N-1 video gens per chain, doubled if mobile is included); always check the skill's stated cost estimate before approving generation.
- Skipping the interview's budget/tier step by rushing straight to "just build it" — the render tier and stills source materially change both cost and visual quality, and are meant to be a deliberate choice up front.
- Using it for a page that needs live interactivity (rotate/zoom on demand) — this produces a fixed, pre-rendered flight path; for interactive 3D use R3F directly (`06-3D/R3F.md`).

## Official links

- GitHub: https://github.com/oso95/scroll-world
