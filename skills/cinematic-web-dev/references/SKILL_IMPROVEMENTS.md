# 🔍 Comprehensive Audit: All Issues, Failures & Technical Learnings (VELORIA Project)

---

## Executive Overview

This audit captures **100% of all technical, procedural, and visual learnings** extracted from building **VELORIA** (Luxury Jewelry AI Website Engine) using `@/cinematic-web-dev`. 

It documents **7 distinct failure modes and technical gotchas** along with their exact remedies in the reference suite.

---

## 🚨 The 7 Complete Learnings & Failure Modes Extracted

### 1. The "Greedy Completion" Failure (Scaffolded 8 Sections at Once)
- **What Happened**: When given the prompt to build VELORIA, the AI generated 8 complete sections (`Hero`, `TheSparkStory`, `MaterialsShowcase`, `CraftsmanshipSection`, `Interactive3DCustomizer`, `CollectionGrid`, `VIPAtelierModal`, `Footer`) in a single turn.
- **Why it Happened**: The AI's default completion bias bypassed descriptive suggestions and generated everything at once, producing shallow filler UI.
- **Remedy**: Documented in `references/HARD_CHECKPOINTS.md` (4 Mandatory Checkpoints with `🛑 HARD STOP` triggers).

---

### 2. The "Toy Primitive 3D" Failure (`OctahedronGeometry` & `TorusGeometry`)
- **What Happened**: When building the 3D diamond ring, the AI generated procedural Three.js primitives (`OctahedronGeometry` + `TorusGeometry`). The result looked like a 1990s low-poly CAD demo rather than Place Vendôme luxury.
- **Why it Happened**: The skill lacked asset quality rules and did not forbid raw geometric code for luxury hero scenes.
- **Remedy**: Documented in `references/EDITORIAL_DESIGN_SYSTEM.md` (Ban untextured Three.js primitives; require photorealistic GLTF/GLB models, GLSL shaders, HDRI lighting, or WebP frame sequences).

---

### 3. The "Video Element Shortcut" Failure (`HTMLVideoElement` vs. WebP Canvas Sequence)
- **What Happened**: Initially, the AI bound scroll position to `video.currentTime` on a raw MP4 file instead of running the frame extraction pipeline. This caused video stuttering, frame dropping on scroll, and browser playback locks.
- **Why it Happened**: The AI took a shortcut using `<video>` instead of pre-extracting WebP image frames.
- **Remedy**: Documented in `references/FRAME_SEQUENCE_PIPELINE.md` (Python OpenCV `extract_frames.py` script + HTML5 `<canvas>` rendering engine with `requestAnimationFrame`).

---

### 4. The CSS Sticky Breaking Failure (`overflow-x-hidden`)
- **What Happened**: The scrollytelling section disappeared on scroll because `App.tsx` had `overflow-x-hidden` on its root wrapper container.
- **Why it Happened**: In standard CSS, `position: sticky; top: 0;` fails completely if any parent container has `overflow-x: hidden` or `overflow: hidden`.
- **Remedy**: Documented in `references/FRAME_SEQUENCE_PIPELINE.md` and `references/EDITORIAL_DESIGN_SYSTEM.md` (Never place `overflow-x: hidden` on parent containers of sticky elements).

---

### 5. Technical Bias vs. Aesthetic Excellence ("AI Template Look")
- **What Happened**: The generated site had generic pill badges (`AI Pipeline`, `Live 3D`), centered text blocks, standard card grids, and cookie-cutter SaaS layouts.
- **Why it Happened**: 90% of skill constraints focused on technical metrics (Lighthouse 90+, 1 canvas context) and 0% on visual design standards.
- **Remedy**: Documented in `references/EDITORIAL_DESIGN_SYSTEM.md` (Editorial typography scaling 80px+ display serif with 10px tracking-[0.3em] uppercase metadata, 1px rule lines, asymmetrical split-screens).

---

### 6. Sub-Skill & MCP Isolation Failure
- **What Happened**: The AI executed `cinematic-web-dev` in isolation without chaining `brainstorming`, `writing-plans`, or Playwright MCP tool checks.
- **Why it Happened**: The skill lacked a mandatory tool/sub-skill handshake protocol.
- **Remedy**: Documented in `references/HARD_CHECKPOINTS.md` (Mandatory sub-skill invocation rules before coding).

---

### 7. Windows Vite `EBUSY` Binary File Locking Technical Gotcha
- **What Happened**: When Vite watched binary video files (`.mp4`) or large image sequence folders (`public/sequence/*.webp`), Windows thrown `EBUSY` file locking errors during hot module replacement.
- **Remedy**: Configure `vite.config.ts` to explicitly ignore binary media files from HMR watching:
  ```ts
  export default defineConfig({
    server: {
      watch: {
        ignored: ['**/*.mp4', '**/sequence/**'],
      },
    },
  });
  ```

---

## 📁 Complete Reference Suite Index

1. **`references/SKILL_IMPROVEMENTS.md`** (This file): Master audit of all 7 learnings.
2. **`references/HARD_CHECKPOINTS.md`**: 4 Gatekeeping Checkpoints protocol.
3. **`references/EDITORIAL_DESIGN_SYSTEM.md`**: High-luxury design standards.
4. **`references/FRAME_SEQUENCE_PIPELINE.md`**: OpenCV extraction & Canvas engine guide.
