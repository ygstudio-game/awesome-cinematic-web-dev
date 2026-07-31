# AI Skills for cinematic web work

**What "skills" means here:** Reusable instruction sets (Claude Skills, or equivalent custom rules/prompts in Cursor/Windsurf) that get loaded before generation to bias output toward better design taste and production quality — instead of re-explaining the same design principles in every prompt.

The original stack plan names five skill categories. Treat these as **categories to fill with whatever skill implementations are available in your tooling** — exact skill names/availability vary by platform and change over time; verify what's actually installed before relying on one by name.

## The five categories

1. **Taste / design judgment** — biases generated layouts, spacing, and color choices toward restrained, premium design rather than generic AI-default UI (centered hero + 3 cards + gradient blob).
2. **UX rigor / design-system generation** — enforces accessibility, focus states, touch target sizing, and interaction feedback that's easy to skip when optimizing purely for visual polish. See `02-AI/UIUXProMax.md` for a concrete, installable implementation (UI/UX Pro Max Skill — style/color/typography reasoning engine).
3. **Responsive craft** — enforces that every component is designed mobile-first and tested at real breakpoints, not just scaled down from a 1440px design.
4. **Web quality / performance discipline** — the Lighthouse-mindset constraints from `08-Optimization/` applied automatically during generation, not bolted on after.
5. **Domain-specific style skills** (e.g. an "Emil Kowalski"-style skill referencing a specific animator/designer's aesthetic) — used for matching a very particular visual voice; optional, apply only when you actually want that specific look.

## How to use them in Claude Code

```bash
claude skill install <skill-name>
```

Or place custom skill definitions in your project/user skills directory per Claude Code's skills documentation, then invoke explicitly:

> "Using the taste and responsive-craft skills, build the hero section per 09-Prompts/AppleStyle.md"

## Common mistakes

- Stacking too many style-opinionated skills at once — taste and a specific designer-voice skill can pull output in conflicting directions; use one aesthetic-defining skill at a time.
- Assuming skill names from any single source (including this handbook) are guaranteed to exist in your current tool version — always verify by listing installed/available skills first.

## Official links

- Claude skills docs: https://docs.claude.com/en/docs/claude-code
