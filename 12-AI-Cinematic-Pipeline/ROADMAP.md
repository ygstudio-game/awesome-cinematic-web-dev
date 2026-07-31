# Roadmap

This module is intentionally manual at the video-generation step today (`07-Video-Generation.md`), for the reasons explained there — provider quality/pricing/availability moves too fast to lock this pipeline to one API.

## Phase 1 (current)

AI generates the Brand Analysis, Creative Brief, storyboard, and image/video prompts. The user generates images and video manually with a provider of their choice, and uploads the results back into the pipeline for optimization, frame extraction, and website generation.

## Phase 2

Optional integrations with video-generation APIs (Veo, Kling, Runway, etc.) for one-click generation where a stable, reasonably-priced API is available — kept optional, not a replacement for the manual path, since provider availability/terms vary by region and account tier.

## Phase 3

Full orchestration: provider selection, asset generation, optimization, website creation, testing, and deployment run end-to-end from a single approved Creative Brief, with human review checkpoints only at the Brand Analysis and Creative Brief stages (the two steps most worth a human reading in full, per `02-Brand-Analysis.md` and `03-Creative-Director.md`).

## Why this phasing

This keeps the module practical today — every step works right now with tools that already exist — while making clear how it evolves as AI video APIs stabilize. Nothing in Phase 2/3 changes the Phase 1 architecture (Creative Brief as single source of truth); later phases only automate steps that are manual today, they don't change what feeds what.
