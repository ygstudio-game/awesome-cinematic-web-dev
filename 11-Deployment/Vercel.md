# Deploying to Vercel

**Why Vercel:** Built by the Next.js team — zero-config deploys, automatic image optimization (`next/image`) at the edge, preview deployments per PR, and edge-network video/asset delivery that matters directly for the video/3D-asset-heavy sites in this handbook.

## Deploy

```bash
npm install -g vercel
vercel login
vercel        # first deploy, follow prompts
vercel --prod # promote to production
```

Or connect the GitHub repo at https://vercel.com/new for automatic deploys on push.

## Config notes for this stack

- Large model/video assets in `public/` count toward Vercel's deployment size limits — for a heavy 3D/video site, consider hosting large binary assets (`.glb`, `.mp4`) on a CDN/object storage (Vercel Blob, Cloudflare R2, S3) and referencing by URL instead of bundling in `public/`.
- Set `images.remotePatterns` in `next.config.ts` if assets come from external storage, or `next/image` optimization will reject them.
- Enable Vercel Analytics/Speed Insights to track real-user Core Web Vitals post-launch — Lighthouse audits (`08-Optimization/Lighthouse.md`) are a lab proxy; field data catches issues lab testing misses (e.g. real device/network diversity).

## Common mistakes

- Committing large uncompressed video/model source files to the repo — bloats every deploy and clone; keep only optimized output in the repo (see `06-3D/Blender.md`, `08-Optimization/Video.md`), or use external storage entirely.
- Not testing preview deployments on real mobile devices before merging — preview URLs are the right place to catch mobile performance regressions before they hit production.

## Official links

- https://vercel.com/docs
