# ReactBits

**What it is:** A large collection of animated React components organized by category — text animations, backgrounds, buttons, cards — each ships as copy-paste source, available in JS or TS and with different animation-engine variants (some Motion-based, some GSAP-based, some CSS-only).

**When to use it:** Text reveal/scramble effects, animated backgrounds (mesh gradients, particles, grid distortion), small interaction details (magnetic buttons, animated cursors).

**When to avoid:** Don't use it as your primary layout/component system — it's a details library, not a design system; pair it with MagicUI/21st.dev/shadcn for structural components.

## Install

Copy-paste per component from https://reactbits.dev, or install via the CLI:

```bash
npx jsrepo add https://reactbits.dev/default/TextAnimations/SplitText
```

Or via ReactBits MCP (`03-MCP/ReactBits.md`) for agent-driven install.

## Common mistakes

- Grabbing a GSAP-variant component into a Motion.dev-standardized project without checking — ReactBits explicitly offers both engine variants per component; always select the Motion/CSS variant unless you've deliberately opted into GSAP (`01-Setup/GSAP.md`).
- Overusing text-scramble/glitch effects on body copy — reserve for headlines/hero text, not paragraphs (readability + performance).

## Official links

- https://reactbits.dev
- GitHub: https://github.com/DavidHDev/react-bits
