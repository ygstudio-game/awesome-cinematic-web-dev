# Basement Studio scrollytelling patterns

**What it is:** Not a single installable package — a reference to the scrollytelling approach popularized by Basement Studio's award-winning sites (webgl/canvas-driven scroll narratives with heavy use of R3F + custom scroll-sync code). Used here as a *pattern reference*, not a library.

**Why it's in this handbook:** When ScrollyVideo (pre-rendered) and Scrollama (step-based) both fall short — you want a *live* WebGL scene that scrubs continuously with scroll, combining the visual richness of Basement Studio-style sites — the pattern is: R3F scene + Theatre.js sequence + Lenis scroll progress, exactly as documented in `05-Animation/Theatre.md`.

## The composite pattern

```
Lenis (scroll progress, 0 → 1 per section)
   → drives Theatre.js sequence.position (05-Animation/Theatre.md)
        → which animates R3F scene properties, camera, materials (06-3D/R3F.md)
   → optionally also drives Motion.dev DOM overlay text (05-Animation/Motion.md)
```

This is the "hard mode" storytelling technique — most sites should reach for ScrollyVideo or Scrollama first (cheaper to build and maintain); use this composite only for a genuine flagship hero moment where interactivity or a live camera path is worth the added engineering cost.

## Study, don't copy

Look at Basement Studio's own site and case studies for the actual sequencing/timing craft — the mechanics are documented here, but the pacing and restraint (what *not* to animate) is a design judgment call best learned by studying real examples. See `Resources.md` → Inspiration.

## Common mistakes

- Reaching for this full composite pattern by default — it's the most expensive to build/maintain of all the storytelling options in this section; justify it against ScrollyVideo/Scrollama first.
- Building the live-scene version without ever validating performance on mid-tier mobile — this pattern has the highest performance risk in the whole handbook (live WebGL + continuous scroll-driven state updates).
