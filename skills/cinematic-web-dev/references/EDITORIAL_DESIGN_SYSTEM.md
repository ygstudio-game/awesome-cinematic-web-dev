# 🎨 Editorial Luxury Design System Guide

---

## Overview

High luxury digital boutiques (Cartier, Tiffany & Co., Place Vendôme ateliers) do **NOT** look like SaaS landing pages. They rely on **extreme typography contrast, asymmetrical split-screen layouts, 1px gold/white rule lines, and generous unhurried whitespace**.

This reference defines the visual rules required to prevent AI agents from generating generic "AI template UI".

---

## 1. Typography Hierarchy & Ratios

| Component | Font Style | Size (Desktop / Mobile) | Tracking / Letter Spacing | Case |
|---|---|---|---|---|
| **Display Title** | Cormorant Garamond / Playfair Display (Serif) | `72px – 120px` / `44px` | `tracking-wide` | Title Case |
| **Section Headline** | Editorial Serif | `40px – 64px` / `32px` | `tracking-wide` | Title Case |
| **Metadata Tag / Act** | Mono / Sans-serif | `10px – 11px` | `tracking-[0.3em]` | UPPERCASE |
| **Body Narrative** | Inter / Outfit (Light 300) | `14px – 16px` | `tracking-normal` | Sentence Case |
| **Numeric Metrics** | High-Contrast Serif | `36px – 56px` | `tracking-tight` | Numeric |

---

## 2. Layout Architecture: Asymmetrical Pinned Split-Screens

### ❌ Generic SaaS Layout (Banned for Luxury)
- Centered paragraph sitting over a background video.
- Grid of 3 identical rectangular cards with neon glow borders.
- Pill badges (`AI Powered`, `New Feature`) floating everywhere.

### ✅ Luxury Editorial Split-Screen Layout (Required)
```
┌───────────────────────────────────────┬───────────────────────────────────────┐
│                                       │  ACT I — PRIMORDIAL CARBON            │
│                                       │  ───────────────────────────────────  │
│                                       │  Forged in Deep Earth                 │
│         PINNED MEDIA / CANVAS         │                                       │
│          (WebP Frame Scrubbing)       │  150 kilometers beneath the mantle,   │
│                                       │  intense heat crystallizes carbon     │
│                                       │  into an indestructible diamond.      │
│                                       │                                       │
│                                       │  1.2 GPa          Refractive 2.417    │
│                                       │  Mantle Pressure  Total Internal Fire │
└───────────────────────────────────────┴───────────────────────────────────────┘
```

---

## 3. Dark Luxury Color Palette Tokens

- **Obsidian 950 (Background)**: `#0B0C10` (Deep obsidian dark sky, not pure black `#000000`).
- **Champagne Gold (Accent)**: `#D4AF37` / `#F3E5AB` (Subtle metallic warm gold).
- **Studio Spotlight Gradient**: `radial-gradient(circle at center, rgba(212,175,55,0.08) 0%, transparent 70%)`.
- **Rule Lines**: `border-white/10` or `border-gold-500/20` (1px ultra-thin lines).

---

## 4. Prohibited UI Elements (Banned List)

- ❌ **No Raw Three.js Primitives**: Never use untextured `TorusGeometry`, `OctahedronGeometry`, or `BoxGeometry` for product showcases.
- ❌ **No SaaS Pill Badges**: Avoid rounded blue/purple SaaS pill badges with icons.
- ❌ **No Heavy Box Shadows / Neon Glows**: Luxury uses subtle lighting gradients and thin rule lines instead of bright drop-shadows.
- ❌ **No Crowded Grids**: Maintain generous margin padding (`px-8 lg:px-20`, `py-16 lg:py-32`).
