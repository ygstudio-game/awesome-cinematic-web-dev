# Antigravity

**What it is:** Google's agentic AI IDE — an editor built around an autonomous coding agent (powered by Gemini) that can plan, write, run, and browser-test code across a whole project with less manual back-and-forth than a chat-style assistant.

**Why it's in this handbook:** It's one of the viable "direct an agent to build this for you" tools alongside Claude Code, Cursor, and Windsurf — good for users who want the agent to work more autonomously through a multi-step build (scaffold → install deps → build sections → self-check in browser) with less step-by-step prompting.

**When to use it over Claude Code:** You want a more autonomous, "run for a while and check back" workflow, or you're already in the Google/Gemini ecosystem. For this specific stack, Claude is the primary recommendation (`02-AI/Claude.md`) because of its long-context coherence across many small config/component files — but Antigravity is a solid alternative, especially for its built-in browser-verification loop, which overlaps with what `03-MCP/Playwright.md` gives Claude Code.

**When to prefer Claude Code instead:** Long, many-file builds where you want tight control and review at each step rather than a longer autonomous run; also if you're relying heavily on Claude Skills (`02-AI/Skills.md`) for design taste, which are Claude-specific.

## Setup

Download from Google's Antigravity site, open the project folder (or let it scaffold a new one).

Give it the same conventions any other agent needs — paste this as your first instruction, or save it as a project rules file if Antigravity supports one:

```
Stack: Next.js App Router, Tailwind v4, Motion.dev, React Three Fiber + Drei, Lenis.
No GSAP unless Motion.dev genuinely cannot achieve the effect.
Only one active <canvas> on screen at a time.
Respect prefers-reduced-motion on every animated component.
Prefer MagicUI / ReactBits / 21st.dev components over hand-rolled UI.
Verify each section in the browser before moving to the next.
```

## Typical workflow

> "Scaffold a Next.js + Tailwind project, install Motion.dev/Lenis/React Three Fiber, then build the hero section from this prompt: [paste from 09-Prompts/AppleStyle.md]. Open it in the browser and check it renders correctly before continuing."

Antigravity's autonomous loop can run through scaffold → install → build → self-verify in one instruction — but for anything beyond a single section, review its output before letting it continue to the next one, same discipline as any other agent (see the README's "Getting the best output" guide).

## Common mistakes

- Giving it one giant instruction for the whole site and walking away — autonomy is powerful but compounds mistakes the same way any agent's does; check the hero before letting it continue.
- Not restating your stack/exclusion constraints — without a persisted rules file, constraints from an earlier session don't automatically carry forward.

## Official links

- https://antigravity.google
