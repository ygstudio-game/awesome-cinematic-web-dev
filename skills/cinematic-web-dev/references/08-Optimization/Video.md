# Video optimization

**Why video over GIF:** GIFs are limited to 256 colors, no inter-frame compression to speak of, and decode on the CPU. MP4/WebM support real compression and hardware-accelerated decode — same or better visual quality at a fraction of the file size.

## Encoding for standard background/hero video

```bash
ffmpeg -i source.mov -vcodec libx264 -crf 23 -preset slow \
  -vf "scale=1920:-2" -an -movflags +faststart hero.mp4

ffmpeg -i source.mov -vcodec libvpx-vp9 -crf 30 -b:v 0 \
  -vf "scale=1920:-2" -an hero.webm
```

Ship both — `<video>` with a `<source>` for WebM first, MP4 fallback:

```html
<video autoplay muted loop playsinline>
  <source src="/hero.webm" type="video/webm" />
  <source src="/hero.mp4" type="video/mp4" />
</video>
```

`-an` strips audio (background/hero videos are almost always silent); `+faststart` moves metadata to the front so playback can start before the full file downloads.

## Encoding for ScrollyVideo (scrub-heavy, `07-Storytelling/ScrollyVideo.md`)

```bash
ffmpeg -i source.mov -vcodec libx264 -crf 20 -preset slow \
  -g 15 -keyint_min 15 \
  -vf "scale=1920:-2" -an -movflags +faststart scrolly.mp4
```

`-g 15 -keyint_min 15` forces a keyframe every 15 frames — scroll-scrubbing seeks to arbitrary frames constantly, and a short GOP (group of pictures) keeps those seeks fast and stutter-free, at the cost of a somewhat larger file than a standard long-GOP encode.

## Common mistakes

- Using a long-GOP, small-file encode (fine for linear playback) for a ScrollyVideo source — causes visible stutter every time the scroll direction reverses between keyframes.
- Autoplaying full-resolution 4K hero video on mobile — serve a smaller `scale`d version via `<source media="...">` or a responsive video component; mobile viewports don't need 4K source.
- Not muting/`playsinline`-ing autoplay video — browsers block autoplay with sound, and `playsinline` is required to avoid forced fullscreen on iOS Safari.

## Official links

- ffmpeg: https://ffmpeg.org
