# Website Generation

**What this step does:** The final generation step — takes the Creative Brief (with its now-filled `storyboard`, `imagePrompts`, `videoPrompts` fields) plus the generated/optimized media, and produces the actual production-ready website.

This prompt is a superset of the ones in root `09-Prompts/` — it additionally requires the Creative Brief and generated assets as input rather than starting from a bare site-type description.

## Prompt

```
You are an Awwwards-winning Creative Developer.

Using:
- Brand Analysis
- Creative Brief
- Storyboard
- Image Assets
- Video Assets

Generate a production-ready website.

Tech Stack:
- Next.js
- TypeScript
- Tailwind
- Motion.dev
- React Three Fiber
- Drei
- Lenis
- ScrollyVideo
- Canvas Animation
- Playwright MCP
- MagicUI MCP
- ReactBits MCP

Generate:
- Folder Structure
- Components
- Animations
- Responsive Design
- Accessibility
- Performance Optimization
- SEO
- Deployment Ready

Maintain Lighthouse score above 95.
```

Attach the actual Creative Brief file (`03-Creative-Director.md`) — not a paraphrase of it — plus the file paths/URLs of the approved stills (`06-Image-Generation.md`) and the frame-sequence manifest (`09-Frame-Extraction.md`) when running this.

## How this maps to the rest of the repo

- **Tech stack** — identical to the root `AGENTS.md` default stack; this doesn't introduce a different stack, it feeds the same one better input.
- **Folder structure** — use `10-Templates/FolderStructure.md` (root) as the scaffold this generates into.
- **"Canvas Animation"** in the stack list — implement per `10-Canvas-Animation.md` (this module) for the frame-sequence hero, alongside or instead of `ScrollyVideo` depending on which technique the Creative Brief's motion system calls for.
- **MCP servers** — set these up per `03-MCP/` (root) *before* running this prompt, so the agent can verify each generated section visually, same discipline as everywhere else in this repo.
- **Hard constraints** (one canvas, `prefers-reduced-motion`, no GSAP/Spline unless justified, dpr cap) — still apply. This prompt doesn't override root `AGENTS.md`'s constraints; both should be given to the agent together.
- **Lighthouse 95+** — matches the stricter end of the root handbook's target range (`08-Optimization/Lighthouse.md`); appropriate here since this is meant to be the flagship, fully-realized output of the whole pipeline.

## Build discipline

Same rule as the rest of this repo: don't run this as one giant generation and walk away. Have the agent build the hero (which consumes the storyboard/media directly) first, verify it in the browser via MCP, then proceed section by section through the rest of the Creative Brief's `websiteArchitecture.sections`.

## Common mistakes

- Running this prompt without the Creative Brief actually attached — produces a generic site that happens to mention the right tech stack, defeating the entire point of the pipeline.
- Treating the listed tech stack as mandatory in full for every project — a portfolio site with no video assets doesn't need `ScrollyVideo`/canvas animation in its stack; drop what the Creative Brief doesn't call for.
- Skipping the Lighthouse check because "the prompt already says maintain 95+" — the instruction shapes generation, it doesn't guarantee the result; verify per `08-Optimization/Lighthouse.md`.
