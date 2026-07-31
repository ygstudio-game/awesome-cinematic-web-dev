# Prompt: Apple-style product page

```
Create a premium Apple-quality product showcase using React Three Fiber.

Requirements:
- React Three Fiber + Drei
- Motion.dev for DOM text/UI reveals
- Lenis for smooth scroll
- Scroll-driven camera move through 3-4 product angles (see 06-3D/R3F.md camera rig pattern)
- Responsive, mobile-optimized — on mobile, replace the live 3D scene with a ScrollyVideo
  fallback (07-Storytelling/ScrollyVideo.md) rather than running WebGL on constrained devices
- Soft studio lighting via Drei's Environment preset
- Floating/idle animation on the product when scroll is not active
- Generous whitespace, large confident typography, minimal color palette
- One claim per screen — do not stack multiple headlines/features in one viewport
- Performance optimized: capped dpr, lazy loaded canvas, one active canvas only
- No GSAP unless Motion.dev genuinely cannot achieve the effect

Avoid:
- Generic gradient blobs, stock 3D card hover effects, centered-hero-with-three-cards layout
- Multiple simultaneous animated elements competing for attention in one viewport

Follow production-quality architecture: typed props, shared easing/timing constants,
composable subcomponents (Hero, CameraRig, ProductModel, ScrollSection).
```

## Why this works

Naming the exact reference (Apple), the exact stack, and explicit exclusions is what prevents regression to generic AI-default UI — see `02-AI/Prompts.md` for the underlying pattern.
