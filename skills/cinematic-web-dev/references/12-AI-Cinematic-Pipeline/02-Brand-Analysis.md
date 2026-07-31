# Brand Analysis

**What it produces:** A structured breakdown of the brand fundamentals behind the user's idea — the raw material the Creative Brief (`03-Creative-Director.md`) is built from.

**Why it's a separate step from the Creative Brief:** Analysis and creative direction are different skills. Asking one prompt to both objectively analyze the brand *and* make creative decisions tends to produce shallower analysis — the model jumps to solutions before it's finished understanding the problem. Splitting them produces a better-grounded Creative Brief.

## Prompt

```
You are a Senior Brand Strategist.

Your job is to analyze the user's website request.

Determine:
- Industry
- Audience
- Brand Personality
- Color Palette
- Typography
- Motion Style
- Visual Language
- Lighting
- Camera Style
- Storytelling Style
- UI Density
- Luxury Level

Produce structured JSON.

Never generate UI.
Never generate code.
Only analyze.
```

## Expected output shape

```json
{
  "industry": "string",
  "audience": { "primary": "string", "psychographics": ["string"] },
  "brandPersonality": ["string"],
  "colorPalette": { "primary": "#hex", "secondary": "#hex", "accent": "#hex", "neutrals": ["#hex"] },
  "typography": { "display": "string", "body": "string", "rationale": "string" },
  "motionStyle": "string",
  "visualLanguage": "string",
  "lighting": "string",
  "cameraStyle": "string",
  "storytellingStyle": "string",
  "uiDensity": "minimal | moderate | dense",
  "luxuryLevel": "1-10"
}
```

## Common mistakes

- Letting this step also decide implementation details (fonts as installable packages, exact Tailwind tokens) — keep it strategic; `03-Creative-Director.md` and `11-Website-Generation.md` handle implementation.
- Skipping straight to the Creative Brief prompt without running this first — the Creative Director prompt is written to consume this JSON as input; running it cold produces a shallower brief.
- Not reviewing the output before proceeding — this is the one manual checkpoint worth actually reading in full, since every later step inherits its mistakes.
