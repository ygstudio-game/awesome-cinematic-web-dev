# Deploying to Cloudflare (Pages / Workers)

**Why Cloudflare:** Cheaper/generous bandwidth for asset-heavy sites (relevant here given video/3D model payloads), global edge network, and Cloudflare R2 (S3-compatible, zero egress fees) is a natural pairing for hosting large video/model assets referenced by URL rather than bundled in the app.

## Deploy (Next.js via @cloudflare/next-on-pages)

```bash
npm install -D @cloudflare/next-on-pages
npx wrangler login
npx @cloudflare/next-on-pages
npx wrangler pages deploy .vercel/output/static
```

Or connect the GitHub repo directly in the Cloudflare dashboard (Workers & Pages → Create → Pages → connect repo) for automatic deploys.

## Hosting large assets on R2

```bash
npx wrangler r2 bucket create cinematic-site-assets
npx wrangler r2 object put cinematic-site-assets/hero.mp4 --file=./hero.mp4
```

Reference via the bucket's public URL (or a custom domain bound to it) from `ScrollyVideo`/`<video>`/`useGLTF` calls instead of `public/` in the repo — keeps the app bundle small and deploys fast (see `11-Deployment/Vercel.md`'s note on the same issue).

## Common mistakes

- Not all Next.js features (some server-side APIs, certain middleware patterns) are fully supported under `next-on-pages` — check current compatibility before committing to Cloudflare if the project relies on advanced App Router server features.
- Forgetting CORS configuration on an R2 bucket when loading assets (e.g. `.glb` via `fetch`/`useGLTF`) cross-origin from the Pages deployment domain.

## Official links

- https://developers.cloudflare.com/pages
- https://developers.cloudflare.com/r2
