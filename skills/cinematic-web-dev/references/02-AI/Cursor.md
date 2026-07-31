# Cursor

**What it is:** A VS Code fork with deep AI-native editing — inline diffs, multi-file agent mode, and codebase-aware chat.

**Why use it:** Fast iteration loop for UI tweaks where you want to see a diff and accept/reject inline, rather than a full agentic session. Good complement to Claude Code for smaller, localized edits (adjusting a Motion.dev easing curve, tweaking Tailwind spacing).

**When to use it over Claude Code:** Quick, contained edits inside a file you already have open. For multi-file architecture work (wiring Theatre.js sequencing through a scroll-driven R3F scene across several components), Claude Code's longer-context agent mode tends to hold up better.

## Setup

Download from https://cursor.com, sign in, open the project folder.

`.cursorrules` (or `.cursor/rules/*.mdc`) at repo root — same idea as `CLAUDE.md`:

```
Stack: Next.js App Router, Tailwind v4, Motion.dev, React Three Fiber, Lenis.
Prefer MagicUI/ReactBits/21st.dev components over hand-rolled UI.
No GSAP unless Motion.dev cannot achieve the effect.
Always guard animated components with prefers-reduced-motion.
```

## Common mistakes

- Running large multi-file refactors in Cursor's chat without checking the diff carefully — its agent mode can touch more files than intended in one pass.
- Not setting project rules — without them Cursor has no memory of your "no GSAP" / "one canvas" constraints between sessions.

## Official links

- https://cursor.com/docs
