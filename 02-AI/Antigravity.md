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

## Installing this handbook's skill

Antigravity is one of the "Universal" agents supported by Vercel's skills CLI, so the install from the root `README.md` works directly:

```bash
npx skills add ygstudio-game/awesome-cinematic-web-dev
```

Select **Antigravity** (and/or **Antigravity CLI** if you use both the IDE and its CLI) at the agent-picker prompt, choose **Project** scope, and confirm. It installs to `.agents/skills/cinematic-web-dev/` in the current project — Antigravity discovers skills there automatically via their description, so no separate registration step is needed.

Once installed, just ask Antigravity for what you want ("build a cinematic Apple-style product page") — it should pick up the skill on its own from the description match. If it doesn't seem to be using it, point it at the file directly: "follow the procedure in `.agents/skills/cinematic-web-dev/SKILL.md`."

If the installer reports `EBUSY: resource busy or locked` on a file under `.agents/skills/`, close Antigravity (or any process with that project open) first, then re-run the same install command — it only needs to retry the agents that failed.

## Typical workflow

> "Scaffold a Next.js + Tailwind project, install Motion.dev/Lenis/React Three Fiber, then build the hero section from this prompt: [paste from 09-Prompts/AppleStyle.md]. Open it in the browser and check it renders correctly before continuing."

Antigravity's autonomous loop can run through scaffold → install → build → self-verify in one instruction — but for anything beyond a single section, review its output before letting it continue to the next one, same discipline as any other agent (see the README's "Getting the best output" guide).

## Common mistakes

- Giving it one giant instruction for the whole site and walking away — autonomy is powerful but compounds mistakes the same way any agent's does; check the hero before letting it continue.
- Not restating your stack/exclusion constraints — without a persisted rules file, constraints from an earlier session don't automatically carry forward.

## Official links

- https://antigravity.google
