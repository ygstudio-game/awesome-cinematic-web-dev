# AI Cinematic Asset Generation Pipeline

This module turns a single website idea into a complete, cohesive set of cinematic visual assets — and then into a production-ready site — with AI acting as Creative Director at every stage. The developer's job shrinks to reviewing and approving what gets generated, not manually producing it.

This is what elevates the rest of this repo from "a curated collection of resources" into a full **AI Cinematic Website Engine**: idea in, deployed premium site out, with a single coherent creative vision running through every asset along the way.

## The core idea: one Creative Brief, not a video-first pipeline

Video generation is one output of this pipeline, not its center. If video generation were the center, every downstream step would have to reinterpret the brand on its own — and that's exactly what produces inconsistent, disjointed results (mismatched color, tone, or motion language between the hero video and the coded site around it).

Instead, everything derives from one artifact:

```
User Idea
      ↓
Brand Analysis
      ↓
Creative Brief  ← single source of truth
      ├── Website Architecture
      ├── UI Design Language
      ├── Color Palette
      ├── Typography
      ├── Motion System
      ├── Storyboard
      ├── Image Prompts
      ├── Video Prompts
      ├── 3D Concepts
      ├── Copywriting
      ├── Performance Budget
      └── SEO Strategy
                ↓
         Website Generation
```

Every step in this module reads from the Creative Brief rather than inventing its own interpretation of the brand. This is what makes the generated site feel cohesive from visuals through implementation — the same reason `02-AI/Claude.md`'s `CLAUDE.md` convention exists elsewhere in this repo, applied to creative decisions instead of just technical ones.

## Why manual video generation (for now)

AI video models differ hugely in quality, pricing, speed, and availability, and the landscape is moving fast. Rather than lock this pipeline to one provider's API, it generates production-quality **prompts** and lets you generate the actual clip with whichever model currently gives the best result — Google Veo, Kling, Runway, Pika, Luma, Hailuo, or whatever comes next. You paste the prompt in, download the clip, and hand it back to the pipeline at the optimization step. See `ROADMAP.md` for where this goes as provider APIs stabilize.

## Full workflow

```
Client idea
    ↓
Research
    ↓
Brand Analysis           (02-Brand-Analysis.md)
    ↓
Creative Brief           (03-Creative-Director.md)
    ↓
Storyboard                (04-Storytelling.md)
    ↓
Image prompts               (05-Prompt-Generation.md)
    ↓
Video prompts                 (05-Prompt-Generation.md)
    ↓
Generate images                 (06-Image-Generation.md — manual, any provider)
    ↓
Generate video                    (07-Video-Generation.md — manual, any provider)
    ↓
Download clip
    ↓
Optimize video                       (08-Video-Optimization.md)
    ↓
Extract frames                          (09-Frame-Extraction.md)
    ↓
Canvas sequence                            (10-Canvas-Animation.md)
    ↓
Generate website                              (11-Website-Generation.md)
    ↓
Motion + performance audit                       (existing 05-Animation/, 08-Optimization/)
    ↓
Deploy                                              (12-Deployment.md)
```

## Files in this module

| File | Purpose |
|---|---|
| `01-Overview.md` | Vision, philosophy, how this module fits the rest of the repo |
| `02-Brand-Analysis.md` | Prompt + schema for analyzing the user's idea into brand fundamentals |
| `03-Creative-Director.md` | Prompt + schema for the Creative Brief — the single source of truth |
| `04-Storytelling.md` | Storyboard generation — splits the hero into 5–10 scenes |
| `05-Prompt-Generation.md` | Converts the storyboard into image and video generation prompts |
| `06-Image-Generation.md` | Where/how to actually generate the stills (Whisk, FLUX, Imagen, Midjourney, SD) |
| `07-Video-Generation.md` | Where/how to actually generate the clips (Veo, Kling, Runway, Pika, Luma, Hailuo) |
| `08-Video-Optimization.md` | Compress/convert the generated clip with ffmpeg |
| `09-Frame-Extraction.md` | Extract a frame sequence + manifest from the optimized clip |
| `10-Canvas-Animation.md` | Render the frame sequence as a scroll-scrubbed canvas animation |
| `11-Website-Generation.md` | The full site-generation prompt, fed by everything above |
| `12-Deployment.md` | Pointer to this repo's existing deployment guides |
| `Resources.md` | Every tool/link referenced in this module |
| `ROADMAP.md` | Where manual-video-today evolves toward automated generation |

## When to use this module vs. the rest of the repo

Use this module when you're starting from a bare idea and want AI to drive brand/creative decisions, not just implementation. If you already have brand assets, a design direction, and just want the coded site, skip straight to `09-Prompts/` and `10-Templates/` elsewhere in this repo — this module's `11-Website-Generation.md` prompt is a superset of those that additionally consumes a Creative Brief and generated media.

See the root `AGENTS.md` for how this module fits into the overall task→file routing.
