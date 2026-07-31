# Storyboard Generation

**What it produces:** A scene-by-scene storyboard for the hero/flagship sequence, derived from the Creative Brief (`03-Creative-Director.md`) — not invented independently.

**Relationship to `07-Storytelling/` (root):** That section documents the *techniques* for playing a scroll-driven sequence (Scrollama for step-based narrative, ScrollyVideo.js for scroll-scrubbed video, `scroll-world` for a fully AI-generated flythrough). This file produces the *content* those techniques play back — the storyboard is technique-agnostic; which root-level technique renders it is a separate decision made in `11-Website-Generation.md`.

## Prompt

```
Create a cinematic storyboard.

Split the hero section into scenes.

Each scene should contain:
- Purpose
- Camera
- Motion
- Timing
- Transition
- Text Placement
- Visual Focus

Return between 5 and 10 scenes.

The storyboard should naturally transition into website sections.
```

Attach the Creative Brief (`03-Creative-Director.md`) when running this — the storyboard's camera style, lighting, and mood must match the brief, not be reinvented.

## Expected output shape

```json
{
  "scenes": [
    {
      "index": 1,
      "purpose": "string",
      "camera": "string",
      "motion": "string",
      "timingSeconds": 3,
      "transition": "string",
      "textPlacement": "string",
      "visualFocus": "string"
    }
  ]
}
```

Write this back into the Creative Brief's `storyboard` field (`03-Creative-Director.md`'s schema) rather than keeping it as a separate disconnected file.

## Common mistakes

- Generating a storyboard that ignores the Creative Brief's stated camera style/mood — always attach the brief, don't run this prompt cold.
- Producing scenes with no natural handoff into the rest of the page — the prompt explicitly asks for the storyboard to transition into website sections; check the last scene actually sets up section 2, not just ending the hero.
- More than ~10 scenes — past that point, per-scene generation cost (`06-Image-Generation.md`, `07-Video-Generation.md`) and total hero runtime both balloon; tighten the story instead of adding scenes.
