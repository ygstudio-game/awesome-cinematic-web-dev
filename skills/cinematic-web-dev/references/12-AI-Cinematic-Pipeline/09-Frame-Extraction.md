# Frame Extraction

**What this step does:** Converts the optimized video (`08-Video-Optimization.md`) into a numbered sequence of still frames plus a manifest describing them — the input `10-Canvas-Animation.md` needs to render a scroll-scrubbed canvas sequence.

## Extract frames

```bash
mkdir -p sequence
ffmpeg -i scene-sequence.mp4 \
  -vf fps=15 \
  sequence/frame_%04d.webp
```

`fps=15` is a reasonable default for scroll-scrubbed playback — scrubbing rarely needs full 30/60fps smoothness since scroll velocity, not frame rate, is what reads as smooth to the user. Raise it only if fast scroll produces visibly choppy motion in testing.

WebP output balances quality and size better than PNG for a sequence that can run into hundreds of frames; use `-q:v 80` to tune:

```bash
ffmpeg -i scene-sequence.mp4 -vf fps=15 -q:v 80 sequence/frame_%04d.webp
```

## Generate a manifest

The canvas animation engine (`10-Canvas-Animation.md`) needs to know frame count, dimensions, and fps without probing every file at runtime:

```bash
ffprobe -v error -select_streams v:0 -show_entries stream=width,height -of csv=p=0 scene-sequence.mp4
```

```bash
# manifest.json
python3 -c "
import json, glob
frames = sorted(glob.glob('sequence/frame_*.webp'))
manifest = {
    'frameCount': len(frames),
    'fps': 15,
    'width': 1920,
    'height': 1080,
    'framePattern': 'sequence/frame_%04d.webp'
}
json.dump(manifest, open('sequence/manifest.json', 'w'), indent=2)
"
```

## Common mistakes

- Extracting at full source fps (often 24-30) for a sequence that will only ever be scroll-scrubbed — inflates total asset count and download size for no perceptible benefit; downsample with `fps=` at extraction time.
- Not generating a manifest and instead hardcoding frame count in the frontend — breaks the moment you regenerate the video with a different length; always derive playback code from the manifest.
- Using PNG for large sequences — file size adds up fast across hundreds of frames; WebP at `-q:v 80` is a better default unless you specifically need transparency + lossless (in which case see `references/knockout.py`-style approaches referenced in `07-Storytelling/ScrollWorld.md`, root).

## Official links

- ffmpeg / ffprobe — https://ffmpeg.org
