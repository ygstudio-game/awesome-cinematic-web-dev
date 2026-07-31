# Overview

Awesome Cinematic Web Dev is no longer just a curated collection of resources. This module turns it into a complete AI-powered workflow for building premium, storytelling-driven, cinematic websites.

The platform guides an AI agent from a simple idea to a fully functional, production-ready website. The workflow covers:

- Brand research
- Creative direction
- Storytelling
- AI prompt engineering
- Image generation
- Video prompt generation
- Manual AI video generation
- Automatic video optimization
- Automatic frame extraction
- Website generation
- Motion system
- Performance optimization
- Deployment

The objective is to minimize manual work while maintaining complete creative control and premium visual quality.

## Philosophy

```
Idea
  ↓
Strategy
  ↓
Story
  ↓
Assets
  ↓
Website
  ↓
Optimization
  ↓
Deployment
```

Each arrow is a handoff between an AI-generated artifact and the next step that consumes it — never a step reinventing brand/creative decisions the previous step already made. That discipline is enforced by routing everything through the Creative Brief (`03-Creative-Director.md`), not by any single step's good judgment alone.

## How this relates to the rest of the repo

This module produces the *inputs* — brand direction, storyboard, prompts, generated media, frame sequences — that feed the techniques already documented elsewhere:

| This module's output | Consumed by |
|---|---|
| Creative Brief's Motion System | `05-Animation/` |
| Creative Brief's 3D Concepts | `06-3D/` |
| Storyboard | `07-Storytelling/` (Scrollama, ScrollyVideo, or this module's own canvas-sequence technique) |
| Image/video prompts | `06-Image-Generation.md`, `07-Video-Generation.md` (this module) |
| Creative Brief as a whole | `11-Website-Generation.md`, which is a superset of `09-Prompts/` |
| Frame sequence + manifest | `10-Canvas-Animation.md` |
| Finished site | `08-Optimization/`, `11-Deployment/` (root) |

Nothing in `01-Setup/` through `11-Deployment/` (root) changes — this module sits in front of them, feeding better, more consistent input into the same stack and constraints defined in the root `AGENTS.md`.
