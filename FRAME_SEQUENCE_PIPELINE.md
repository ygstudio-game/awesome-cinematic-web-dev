# 🎬 WebP Frame Extraction & Canvas Sequence Scrubbing Engine

---

## Overview

Binding scroll progress to an MP4 video element (`HTMLVideoElement.currentTime`) causes stuttering, dropped frames, and browser rendering locks.

True Apple-style product reveals scrub **pre-extracted WebP image frames** onto an HTML5 `<canvas>` using `requestAnimationFrame`.

---

## 1. Frame Extraction Script (`extract_frames.py`)

Run this Python script using `OpenCV` (`cv2`) to extract video frames into a WebP sequence and generate `manifest.json`.

```python
import cv2
import os
import json

def extract_frames(video_path, output_dir, target_fps=15, quality=82):
    if not os.path.exists(output_dir):
        os.makedirs(output_dir)

    cap = cv2.VideoCapture(video_path)
    if not cap.isOpened():
        print(f"Error opening video file {video_path}")
        return

    orig_fps = cap.get(cv2.CAP_PROP_FPS)
    total_frames = int(cap.get(cv2.CAP_PROP_FRAME_COUNT))
    width = int(cap.get(cv2.CAP_PROP_FRAME_WIDTH))
    height = int(cap.get(cv2.CAP_PROP_FRAME_HEIGHT))

    frame_interval = max(1, int(round(orig_fps / target_fps)))
    frame_count = 0
    extracted_count = 0

    while cap.isOpened():
        ret, frame = cap.read()
        if not ret:
            break

        if frame_count % frame_interval == 0:
            extracted_count += 1
            frame_filename = os.path.join(output_dir, f"frame_{extracted_count:04d}.webp")
            cv2.imwrite(frame_filename, frame, [cv2.IMWRITE_WEBP_QUALITY, quality])

        frame_count += 1

    cap.release()

    manifest = {
        "frameCount": extracted_count,
        "fps": target_fps,
        "width": width,
        "height": height,
        "framePattern": "/sequence/frame_%04d.webp"
    }

    manifest_path = os.path.join(output_dir, "manifest.json")
    with open(manifest_path, "w") as f:
        json.dump(manifest, f, indent=2)

    print(f"Successfully extracted {extracted_count} WebP frames to {output_dir}")

if __name__ == "__main__":
    extract_frames("public/assets/hero_commercial.mp4", "public/sequence")
```

---

## 2. React HTML5 `<canvas>` Rendering Engine

```tsx
import React, { useEffect, useRef, useState } from 'react';

interface Manifest {
  frameCount: number;
  fps: number;
  width: number;
  height: number;
  framePattern: string;
}

export const CanvasScrollytelling: React.FC = () => {
  const containerRef = useRef<HTMLDivElement>(null);
  const canvasRef = useRef<HTMLCanvasElement>(null);
  const framesRef = useRef<HTMLImageElement[]>([]);
  
  const [manifest, setManifest] = useState<Manifest | null>(null);

  // 1. Load Manifest & Preload Frames
  useEffect(() => {
    fetch('/sequence/manifest.json')
      .then((res) => res.json())
      .then((m: Manifest) => {
        setManifest(m);
        const images: HTMLImageElement[] = [];
        for (let i = 0; i < m.frameCount; i++) {
          const img = new Image();
          img.src = m.framePattern.replace('%04d', String(i + 1).padStart(4, '0'));
          images.push(img);
        }
        framesRef.current = images;
      });
  }, []);

  // 2. High-DPI Cover Scaling Helper
  const drawCover = (ctx: CanvasRenderingContext2D, img: HTMLImageElement, w: number, h: number) => {
    const imgRatio = (img.naturalWidth || 1280) / (img.naturalHeight || 720);
    const canvasRatio = w / h;
    let dw = w, dh = h, ox = 0, oy = 0;

    if (canvasRatio > imgRatio) {
      dh = w / imgRatio;
      oy = (h - dh) / 2;
    } else {
      dw = h * imgRatio;
      ox = (w - dw) / 2;
    }

    ctx.clearRect(0, 0, w, h);
    ctx.drawImage(img, ox, oy, dw, dh);
  };

  // 3. Scroll Loop
  useEffect(() => {
    if (!manifest) return;
    const canvas = canvasRef.current;
    if (!canvas) return;
    const ctx = canvas.getContext('2d');
    if (!ctx) return;

    const render = () => {
      if (!containerRef.current || !manifest) return;
      const rect = containerRef.current.getBoundingClientRect();
      const totalScroll = rect.height - window.innerHeight;
      if (totalScroll <= 0) return;

      const progress = Math.max(0, Math.min(1, -rect.top / totalScroll));
      const frameIdx = Math.min(manifest.frameCount - 1, Math.floor(progress * manifest.frameCount));
      const frameImage = framesRef.current[frameIdx];

      if (frameImage && frameImage.complete) {
        drawCover(ctx, frameImage, canvas.width, canvas.height);
      }
    };

    const handleScroll = () => requestAnimationFrame(render);
    window.addEventListener('scroll', handleScroll, { passive: true });
    render();

    return () => window.removeEventListener('scroll', handleScroll);
  }, [manifest]);

  return (
    <section ref={containerRef} className="relative w-full h-[400vh] bg-obsidian-950">
      <div className="sticky top-0 w-full h-screen overflow-hidden">
        <canvas ref={canvasRef} className="w-full h-full block" />
      </div>
    </section>
  );
};
```
