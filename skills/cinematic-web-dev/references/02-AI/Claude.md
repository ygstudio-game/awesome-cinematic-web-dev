# Claude / Claude Code

**What it is:** Anthropic's coding agent (CLI, IDE extension, or claude.ai/code) — the recommended primary driver for this whole stack.

**Why use it for this project:** Long, coherent context across many files (needed when a component touches Tailwind config, R3F scene, Motion.dev variants, and Theatre.js state all at once), strong adherence to explicit constraints ("no GSAP unless necessary", "one active canvas") when they're stated up front in a prompt or `CLAUDE.md`.

## Setup

```bash
npm install -g @anthropic-ai/claude-code
claude
```

Or use the VS Code / JetBrains extension, or claude.ai/code for a browser-based sandboxed environment.

## Project-level guidance file

Create `CLAUDE.md` at the repo root so every session inherits your constraints without re-stating them:

```markdown
# Project conventions

- Stack: Next.js App Router, Tailwind v4, Motion.dev, React Three Fiber + Drei, Lenis.
- No GSAP unless Motion.dev genuinely cannot do it (see 01-Setup/GSAP.md).
- Only one active <canvas> on screen at a time.
- Respect prefers-reduced-motion on every animated component.
- UI components: prefer MagicUI / ReactBits / 21st.dev over hand-rolled ones — check 04-UI/ first.
```

## Recommended skills for this stack

See `02-AI/Skills.md` for the "Impeccable / Taste / UI-UX Pro Max / Responsive Craft / Web Quality" skill set referenced in the original stack plan — install/enable whichever are available in your Claude setup, and chain them before generation: taste and UX constraints first, then implementation.

## MCP integration

Connect Playwright MCP, shadcn MCP, MagicUI MCP so Claude can inspect the *running* app (not just static code) before making changes — see `03-MCP/`.

## Common mistakes

- Not writing a `CLAUDE.md` — re-explaining the same constraints ("no GSAP", "one canvas") every session wastes turns and gets inconsistently followed.
- Asking for a whole cinematic page in one prompt — break it into hero → scroll section → 3D section → footer, reviewing each before moving on, same as you would with a human collaborator.
- Skipping the MCP/browser step and trusting generated animation code without ever seeing it run.

## Official links

- Docs: https://docs.claude.com/en/docs/claude-code
