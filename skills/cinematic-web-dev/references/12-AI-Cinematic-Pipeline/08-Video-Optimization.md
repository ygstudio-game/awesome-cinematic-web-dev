# Video Optimization

**What this step does:** Compresses and converts the raw AI-generated clip(s) from `07-Video-Generation.md` into a web-ready format, before frame extraction (`09-Frame-Extraction.md`).

This is the pipeline-specific companion to the root handbook's general video guidance in `08-Optimization/Video.md` — that file covers encoding for `<video>`/ScrollyVideo playback; this file covers preparing a clip specifically to be **broken into a frame sequence** for the canvas-animation technique in `10-Canvas-Animation.md`.

## Why not just use EZGIF or a GUI tool

Manual GUI compression tools don't compose into a repeatable pipeline — every project reruns the same manual steps by hand. ffmpeg gives you the same result as a scriptable, versionable command.

## Workflow

```
Raw MP4 (from provider)
    ↓
Compress
    ↓
Convert to consistent format/resolution
    ↓
Extract frames (09-Frame-Extraction.md)
    ↓
Generate manifest
    ↓
Canvas animation (10-Canvas-Animation.md)
```

## Commands

Normalize resolution and compress:

```bash
ffmpeg -i scene-01-raw.mp4 \
  -vf "scale=1920:-2" \
  -vcodec libx264 -crf 20 -preset slow \
  -an -movflags +faststart \
  scene-01-optimized.mp4
```

`-an` strips audio (frame-sequence output has no use for it). `-crf 20` keeps quality high since this file is a source for frame extraction, not final delivery — the individual extracted frames get their own compression pass in `09-Frame-Extraction.md`.

If stitching multiple scene clips into one continuous sequence before extraction:

```bash
ffmpeg -f concat -safe 0 -i scenes-list.txt -c copy scene-sequence.mp4
```

where `scenes-list.txt` contains:

```
file 'scene-01-optimized.mp4'
file 'scene-02-optimized.mp4'
file 'scene-03-optimized.mp4'
```

## Common mistakes

- Compressing too aggressively (`-crf` above ~23) before frame extraction — artifacts introduced here get baked into every extracted frame; keep this pass higher-quality and compress the final extracted frames instead.
- Concatenating scenes with mismatched resolution/frame rate — normalize every clip to the same `scale`/fps *before* concatenating, or the `concat` demuxer will produce glitches at the seams.
- Skipping this step and extracting frames directly from the raw provider export — provider exports are often unnecessarily large/high-bitrate; normalizing first keeps the whole pipeline faster.

## Official links

- ffmpeg — https://ffmpeg.org
