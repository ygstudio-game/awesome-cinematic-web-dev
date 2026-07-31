# Deployment

This module doesn't introduce a separate deployment process — use the root handbook's existing guides:

- `11-Deployment/Vercel.md` (root)
- `11-Deployment/Cloudflare.md` (root)

## The one pipeline-specific consideration: asset hosting

This module's output includes a frame sequence (`09-Frame-Extraction.md`) that can run into hundreds of image files, plus the optimized video source and approved stills. That's a meaningfully larger asset payload than a typical project in this repo.

- Don't commit the raw/intermediate pipeline outputs (raw provider exports, unoptimized clips, full-resolution stills) to the site's repo — keep those in your project working directory or a separate assets store, and ship only the final optimized frame sequence + manifest.
- Host the frame sequence and any large video source on external object storage (Vercel Blob, Cloudflare R2) and reference by URL, exactly as recommended in `11-Deployment/Vercel.md` and `11-Deployment/Cloudflare.md` (root) for large model/video assets — the same reasoning applies here, just with more individual files.
- Set appropriate long-lived cache headers on frame sequence assets — they're immutable once generated for a given build, unlike page content.

## Common mistakes

- Committing an entire `sequence/` folder of hundreds of frames to the site repo — bloats every clone/deploy; see the asset-hosting note above.
- Forgetting CORS configuration on external storage serving the frame sequence to the deployed site's domain — same gotcha noted in `11-Deployment/Cloudflare.md` (root) for R2-hosted 3D assets.
