# Prompt Generation — Image & Video

**What it produces:** Ultra-specific, provider-agnostic image and video generation prompts, one per storyboard scene, derived from the Creative Brief + storyboard rather than written fresh per scene (which is what causes visual drift between scenes).

## Image prompt generator

```
You are an expert prompt engineer.

Convert the storyboard into ultra-realistic image generation prompts.

The prompts should be compatible with:
- Google Whisk
- FLUX
- Imagen
- Midjourney
- Stable Diffusion

Maintain visual consistency.

Output one prompt for every storyboard scene.
```

Attach both the Creative Brief and the storyboard (`03-Creative-Director.md`, `04-Storytelling.md`) — consistency across scenes depends on every prompt pulling the same color palette, lighting, and materials from the brief rather than each scene's prompt inventing its own.

## Video prompt generator

```
Convert the storyboard into cinematic AI video prompts.

Each prompt must contain:
- Subject
- Environment
- Lighting
- Camera
- Lens
- Movement
- Composition
- Atmosphere
- Duration
- Aspect Ratio
- Visual Style
- Motion Speed
- Realism

The prompts should work on Google Veo, Kling, Runway, Pika, Luma without modification.
```

## Why "without modification" matters

A prompt tuned to one provider's quirks often needs rewriting for another. Keeping prompts provider-neutral (explicit subject/camera/lighting/lens language rather than provider-specific syntax) is what makes `07-Video-Generation.md`'s "pick any provider" approach actually work — you're not locked in once you've generated the prompts.

## Where the output goes

Write both sets of prompts back into the Creative Brief's `imagePrompts` and `videoPrompts` fields (`03-Creative-Director.md`'s schema). Each scene now has: purpose/camera/motion (storyboard) + an image prompt + a video prompt, all traceable to the same brief.

## Common mistakes

- Generating video prompts without the image prompts already locked — generate stills first (`06-Image-Generation.md`), since the actual rendered stills are what later frame-lock the video seams (see `07-Video-Generation.md`'s frame-conditioning note) — the prompt alone isn't enough for seam continuity.
- Letting each scene's prompt independently describe the color palette in its own words — reference the Creative Brief's exact hex/palette language so scene-to-scene consistency doesn't drift through paraphrasing.
- Omitting aspect ratio / duration — leaving these to provider defaults produces mismatched clip lengths that are painful to reconcile at the frame-extraction step (`09-Frame-Extraction.md`).
