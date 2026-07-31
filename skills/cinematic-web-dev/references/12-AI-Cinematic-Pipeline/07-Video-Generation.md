# Video Generation

## Why manual video?

The current generation of AI video models differs greatly in quality, pricing, speed, and availability. Instead of locking users to one provider, this pipeline generates production-quality prompts (`05-Prompt-Generation.md`). Users may choose:

- **Google Veo** — https://deepmind.google/technologies/veo
- **Kling** — https://klingai.com
- **Runway** — https://runwayml.com
- **Pika** — https://pika.art
- **Luma** — https://lumalabs.ai
- **Hailuo** (MiniMax) — https://hailuoai.video

or any future AI video model. This ensures long-term compatibility while producing the highest possible visual quality available at the time you build.

## Workflow

1. Take each scene's video prompt (`05-Prompt-Generation.md`) and, where the provider supports image-to-video/first-frame conditioning, feed it the matching approved still from `06-Image-Generation.md` as the starting frame.
2. Generate the clip.
3. Download the MP4.
4. Name/organize consistently with the storyboard scene index, e.g. `assets/clips/scene-01.mp4`.
5. Hand the clip to `08-Video-Optimization.md`.

## Frame-locking seams between scenes

If your storyboard has the camera flowing continuously from scene to scene (no hard cut), generate each scene's clip so its **last frame** matches the **next scene's still** as closely as possible — first/last-frame conditioning on providers that support it (image-to-video with an end-frame target) is what makes a connector transition read as one continuous flight rather than a visible cut. This is the same seam-locking technique referenced in `07-Storytelling/ScrollWorld.md` (root) for fully automated world flythroughs — here it's done manually, scene by scene, against your own approved stills.

## Common mistakes

- Generating all clips with different aspect ratios/durations — lock these in the video prompt (`05-Prompt-Generation.md` explicitly asks for both) before generating, not after.
- Not checking the seam between consecutive clips before moving on — a jarring cut between scene 2 and scene 3 is much cheaper to fix by regenerating scene 3 now than after the whole sequence is assembled.
- Treating this as a one-shot generation — budget for regenerating any given clip 2-3 times to get a seam/motion result that matches the brief; this is normal, not a sign something's wrong with your prompt.

## Cost awareness

Video generation is the most expensive step in this pipeline per unit of output. Check current provider pricing before generating a full multi-scene sequence — regenerating N scenes 2-3 times each adds up fast. Approve the storyboard and stills fully (steps `04` and `06`) before spending on video.
