# Image optimization

## Use `next/image` for everything

```tsx
import Image from 'next/image'

<Image src="/product.png" alt="Product" width={1200} height={800} priority />
```

`next/image` automatically serves modern formats (AVIF/WebP) with fallback, generates responsive `srcset`s, and lazy-loads by default — set `priority` only on the LCP image (usually the hero image), never on images below the fold.

## Textures for R3F (separate from `next/image` — these load through Three.js's own loaders)

```bash
npm install -g @squoosh/cli   # or use gltf-transform's texture-compress for glTF-embedded textures
squoosh-cli --webp '{quality:80}' texture-source.png
```

- Match texture resolution to actual on-screen render size — a 4K texture on a torus knot that renders at 400px on screen is pure waste.
- Use power-of-two dimensions (512, 1024, 2048) for GPU-friendly mipmapping.
- Prefer `.ktx2` (Basis compressed) over raw PNG/JPG for large scenes — smaller download and smaller GPU memory footprint, at the cost of an extra build step (`gltf-transform` handles this, see `06-3D/Blender.md`).

## Common mistakes

- Using `<img>` instead of `next/image` for content images — loses automatic format negotiation, responsive sizing, and lazy loading, all of which directly affect Lighthouse's LCP and CLS scores.
- Not specifying `width`/`height` (or `fill` with a sized container) — causes layout shift (CLS) as the image loads.
- Marking every image `priority` "to be safe" — defeats lazy loading; only the actual LCP element should be `priority`.

## Official links

- https://nextjs.org/docs/app/api-reference/components/image
