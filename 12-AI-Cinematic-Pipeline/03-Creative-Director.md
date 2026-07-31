# Creative Director — the Creative Brief

**What it produces:** The Creative Brief — the single source of truth for the entire build. Every later step (storyboard, prompts, website generation) reads from this document instead of re-deriving brand/creative decisions on its own.

**Why this is the center of the pipeline, not video generation:** If each downstream step (storyboard, image prompts, video prompts, website code) independently reinterprets the brand, the result is visually and tonally inconsistent — a hero video that doesn't match the coded site's color system, a storyboard that doesn't match the copywriting voice. Routing everything through one brief is what keeps a multi-stage AI-generated build cohesive.

## Prompt

```
You are an award-winning Creative Director.

Using the Brand Analysis, create the visual concept for the website.

Determine:
- Hero Scene
- Environment
- Camera Movement
- Lighting
- Materials
- Mood
- Animation Style
- Transitions
- Scroll Behavior
- Cinematic References

Output a Creative Brief.

Do not generate implementation code.
```

## The full Creative Brief schema

Extend the prompt's raw output into this complete structure — this is what every later step in the pipeline (and `11-Website-Generation.md`) consumes as input:

```json
{
  "websiteArchitecture": { "pages": ["string"], "sections": ["string"], "navigationModel": "string" },
  "uiDesignLanguage": "string",
  "colorPalette": { "primary": "#hex", "secondary": "#hex", "accent": "#hex" },
  "typography": { "display": "string", "body": "string" },
  "motionSystem": { "easing": "string", "pacing": "restrained | energetic", "signatureMoments": ["string"] },
  "storyboard": null,
  "imagePrompts": null,
  "videoPrompts": null,
  "threeDConcepts": ["string"],
  "copywriting": { "voice": "string", "tagline": "string" },
  "performanceBudget": { "lighthouseTarget": 95, "maxHeroPayloadMB": 5 },
  "seoStrategy": { "primaryKeywords": ["string"], "metaStrategy": "string" }
}
```

`storyboard`, `imagePrompts`, and `videoPrompts` start `null` — they're filled in by `04-Storytelling.md` and `05-Prompt-Generation.md`, which append their output back into this same document rather than producing a disconnected artifact. By the time you reach `11-Website-Generation.md`, this one JSON/markdown file has every field the site generator needs.

## How to use it

Save the Creative Brief as a file in your project (e.g. `creative-brief.json`) and hand it — not a re-summarized version of it — to every subsequent prompt in this pipeline and to your AI agent's conventions file (`02-AI/Claude.md`'s `CLAUDE.md` pattern, root repo).

## Common mistakes

- Treating the Creative Brief as a one-time document you read once — it should be attached/referenced in every subsequent prompt in this pipeline, not summarized from memory by whichever agent session comes next.
- Letting `11-Website-Generation.md`'s prompt run without the actual Creative Brief attached — this is exactly the failure mode this whole module exists to prevent.
- Regenerating the Creative Brief mid-project when one section needs a tweak — patch the specific field instead; regenerating the whole brief risks drifting every other field too.
