# Image Generation

**What this step is:** Manual — you take the per-scene image prompts from `05-Prompt-Generation.md` and generate the actual stills with a provider of your choice. This step isn't automated for the same reason video isn't (`07-Video-Generation.md`'s "why manual" note) — provider quality/pricing/availability shifts fast, and locking to one API would date this pipeline quickly.

## Providers the prompts are written for

- **Google Whisk** — https://labs.google/whisk
- **FLUX** (Black Forest Labs) — https://blackforestlabs.ai
- **Imagen** (Google) — https://deepmind.google/technologies/imagen
- **Midjourney** — https://www.midjourney.com
- **Stable Diffusion** — https://stability.ai

## Workflow

1. Take each scene's image prompt (already written to consistent visual language per `05-Prompt-Generation.md`).
2. Generate the still with your chosen provider.
3. If a still doesn't match the brief's color palette/mood closely enough, regenerate with the same prompt rather than hand-editing the prompt per attempt — preserves consistency with the other scenes.
4. Save stills in a predictable location, e.g. `assets/scenes/scene-01.png` through `scene-N.png`, matching the storyboard's scene indices.

## Consistency across scenes

The biggest risk at this step is scene-to-scene visual drift — scene 3 rendered with slightly different lighting/color than scene 1. Mitigate by:
- Using the same provider for all scenes in one storyboard where possible (mixing providers increases drift risk).
- Reusing a reference image (the first scene's approved still) as an image-prompt input for later scenes, on providers that support it — locks palette/style rather than relying on text description alone.
- Reviewing all stills side-by-side before proceeding to video generation, not one at a time.

## Common mistakes

- Approving stills one at a time instead of reviewing the full set together — drift is much easier to spot side-by-side.
- Regenerating with a modified prompt instead of the same prompt — small prompt edits compound into visible scene-to-scene inconsistency.
- Skipping straight to video generation without stills — the stills are what frame-lock the video seams downstream (see `07-Video-Generation.md`); they aren't optional intermediate output.

## Official links

- See `Resources.md` (this module) for the full link list.
