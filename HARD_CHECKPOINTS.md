# 🛑 Mandatory Gatekeeping Checkpoints Protocol

---

## Overview

AI coding agents naturally suffer from **Greedy Completion Bias**—the tendency to generate 8+ site sections in a single response turn without pausing for user feedback.

This document defines the **4 Mandatory Gatekeeping Checkpoints**. Every AI agent executing `@/cinematic-web-dev` MUST stop for user confirmation at each checkpoint before proceeding to write code for subsequent sections.

---

## Checkpoint Protocol Diagram

```
┌──────────────────────────────────────────────────────────┐
│ CHECKPOINT 1: Brainstorming & Brand Strategy (HARD STOP)  │
└────────────────────────────┬─────────────────────────────┘
                             │
                             ▼
┌──────────────────────────────────────────────────────────┐
│ CHECKPOINT 2: Environment & MCP Handshake                 │
└────────────────────────────┬─────────────────────────────┘
                             │
                             ▼
┌──────────────────────────────────────────────────────────┐
│ CHECKPOINT 3: Hero Section Only + User Review (HARD STOP) │
└────────────────────────────┬─────────────────────────────┘
                             │
                             ▼
┌──────────────────────────────────────────────────────────┐
│ CHECKPOINT 4: Incremental Section-by-Section Lock        │
└──────────────────────────────────────────────────────────┘
```

---

## 1. CHECKPOINT 1 — Brand Strategy & User Brainstorming (HARD STOP)

- **When it runs**: First step of any new project or major feature.
- **Action**:
  1. Execute `references/12-AI-Cinematic-Pipeline/` (Brand Analysis $\rightarrow$ Creative Brief $\rightarrow$ Storyboard).
  2. Define Brand Name, Tagline, Visual Aesthetic (e.g. Dark Luxury, Studio Spotlights), and Chapter Narrative outline.
- **🛑 HARD STOP TRIGGER**:
  - Present the Brand Concept, Palette, and Storyboard sequence to the USER.
  - Ask: *"Does this creative direction match your vision?"*
  - **DO NOT write any project code until the user approves Checkpoint 1.**

---

## 2. CHECKPOINT 2 — Environment & MCP Setup

- **When it runs**: Immediately after Checkpoint 1 approval.
- **Action**:
  1. Verify active MCP tools (Playwright browser preview, shadcn).
  2. Write project conventions file (`CLAUDE.md`) per `references/AGENTS.md`.
  3. Scaffold folder structure per `references/10-Templates/FolderStructure.md`.

---

## 3. CHECKPOINT 3 — Hero Section Only + User Review (HARD STOP)

- **When it runs**: After scaffolding is complete.
- **Action**:
  1. Build ONLY the Hero section component (`Hero3DCanvas.tsx` or Hero frame sequence).
  2. Verify visually using Playwright/Browser screenshot.
- **🛑 HARD STOP TRIGGER**:
  - Present the Hero preview screenshot to the USER.
  - Ask: *"How is the visual quality, typography, and motion performance of this Hero section?"*
  - **DO NOT generate Section 2 until the user approves Checkpoint 3.**

---

## 4. CHECKPOINT 4 — Incremental Section-by-Section Lock

- **When it runs**: After Hero approval.
- **Action**:
  1. Build subsequent sections **ONE AT A TIME** (e.g., Scrollytelling section next, verify, get user approval, then proceed).
  2. Never scaffold 5+ generic filler sections in a single response turn.

---

## 🚨 Anti-Patterns & Red Flags

- ❌ Generating 3+ sections in a single turn without stopping for user feedback.
- ❌ Skipping the Brainstorming / Creative Brief checkpoint.
- ❌ Scaffolding placeholder cards across the whole site instead of polishing 1 component to perfection.
