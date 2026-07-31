# Codex (OpenAI)

**What it is:** OpenAI's coding agent (CLI and cloud), comparable in role to Claude Code — an agentic loop that can read, edit, and run code in your repo.

**Why it's in this handbook:** Useful as a second opinion / cross-check on generated components, or if your team already has OpenAI tooling in place. The stack and constraints documented across this handbook (no GSAP unless necessary, one active canvas, `prefers-reduced-motion`) apply the same regardless of which agent executes them — restate them via an `AGENTS.md`-style file at repo root if you use Codex alongside Claude.

**When to use it over Claude:** Team preference/existing OpenAI subscription. For this specific stack, Claude's longer-context coherence across many small config/component files (per the ChatGPT comparison that seeded this handbook) is the reason it's the primary recommendation — treat Codex as a valid alternative, not a downgrade.

## Setup

```bash
npm install -g @openai/codex
codex
```

## Common mistakes

- Letting two agents (e.g. Codex and Claude Code) edit the same files in the same session without committing between runs — diverging edits are hard to reconcile.

## Official links

- https://developers.openai.com/codex
