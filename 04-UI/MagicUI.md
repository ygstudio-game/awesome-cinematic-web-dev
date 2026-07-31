# MagicUI

**What it is:** A library of animated, Tailwind + Motion-based React components (marquees, animated beams, bento grids, particle effects, borders) distributed via a shadcn-compatible CLI.

**When to use it:** Hero sections, feature/bento grids, animated borders/beams connecting elements, marketing-site "wow" details.

**When to avoid:** Don't reach for it for basic form controls/inputs — use plain shadcn/ui for those and save MagicUI for the pieces where motion is the point.

## Install

Per component, via the registry CLI (no single package install — copy-in model):

```bash
npx shadcn@latest add "https://magicui.design/r/marquee.json"
```

Or browse/install through MagicUI MCP (`03-MCP/MagicUI.md`) so your agent picks the right component and current URL.

## Example usage

```tsx
import { Marquee } from '@/components/ui/marquee'

export function LogoWall({ logos }: { logos: string[] }) {
  return (
    <Marquee pauseOnHover className="[--duration:30s]">
      {logos.map((src) => <img key={src} src={src} alt="" className="h-8 mx-8" />)}
    </Marquee>
  )
}
```

## Common mistakes

- Copying a MagicUI component without updating its color/spacing to your `@theme` tokens (`01-Setup/Tailwind.md`) — looks visibly "bolted on" against the rest of the site.
- Using multiple heavy particle/beam effects on one page — each is cheap alone, but they compound on lower-end devices; budget one hero-level effect per viewport.

## Official links

- https://magicui.design
- GitHub: https://github.com/magicuidesign/magicui
