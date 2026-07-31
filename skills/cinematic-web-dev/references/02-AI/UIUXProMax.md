# UI/UX Pro Max Skill

**What it is:** An AI skill that adds design intelligence to UI/UX generation — a reasoning engine that picks a coherent design system (style, color palette, typography, layout rules) for whatever you're building instead of leaving those choices to the model's generic defaults. This is the concrete implementation behind the "UI UX Pro Max Skill" named as a must-have in this handbook's `02-AI/Skills.md`.

**Why it matters for this stack:** Most of what makes AI-generated UI look generic isn't bad code — it's inconsistent, uncommitted design decisions (a random accent color, a default font pairing, no real style point of view). This skill forces a single coherent system up front, which is exactly the gap between "functional" and "premium" that this whole handbook is chasing.

**Core capabilities (v2.0):**
- 84 UI styles (Glassmorphism, Claymorphism, Minimalism, Brutalism, Neumorphism, etc.)
- 192 color palettes matched to product type
- 74 font pairings (Google Fonts)
- 161 industry-specific reasoning rules for automatic design-system generation
- 22 supported tech stacks (React, Vue, Svelte, SwiftUI, Flutter, etc.)

**When to use it:** Right after you've decided the site type (`09-Prompts/`) but before generating the first section — let it commit to a style/palette/type system, then generate every section against that system.

## Install

**Claude Code plugin marketplace:**

```bash
/plugin marketplace add nextlevelbuilder/ui-ux-pro-max-skill
/plugin install ui-ux-pro-max@ui-ux-pro-max-skill
```

**CLI (recommended, works across agents):**

```bash
npm install -g ui-ux-pro-max-cli
uipro init --ai claude   # or cursor, windsurf, etc.
```

**NPX (no global install):**

```bash
npx ui-ux-pro-max-cli init --ai claude
```

## Requirements

- Python 3.x (standard library only — no network calls or extra installs).
- Node.js/npm for the CLI installer.

## Typical workflow

> "Using the UI/UX Pro Max skill, generate a design system for a [SaaS product / agency / portfolio] site targeting [industry] — then build the hero section from `09-Prompts/` against that system."

The skill recommends style/color/typography, generates matching code, and checks output against anti-patterns — pair it with this handbook's explicit stack/exclusion constraints (`02-AI/Prompts.md`) rather than letting it choose the stack too; it's a design-system reasoning layer, not a replacement for the Next.js/Motion.dev/R3F stack decisions elsewhere in this repo.

## Common mistakes

- Letting it pick a style *and* separately hand-picking one yourself in the same session — commit to one source of truth for the design system per project.
- Skipping it for multi-section builds and re-deriving color/type choices per prompt — this is exactly the inconsistency it exists to prevent; run it once per project, early.

## Official links

- GitHub: https://github.com/nextlevelbuilder/ui-ux-pro-max-skill
