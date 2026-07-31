# Tailwind CSS

**What it is:** Utility-first CSS framework. Styles live as classes in markup instead of separate stylesheets.

**Why use it:** Every UI kit in this handbook (MagicUI, ReactBits, Aceternity, 21st.dev) ships Tailwind-based components — using Tailwind means you can copy-paste their code directly instead of translating class names to CSS-in-JS or modules.

**When to use it:** Always, alongside any of the UI kits in `04-UI/`.

## Install

If you used `create-next-app` with the Tailwind prompt set to Yes, it's already configured. For a manual/existing project:

```bash
npm install tailwindcss @tailwindcss/postcss postcss
```

`postcss.config.mjs`:

```js
export default {
  plugins: { '@tailwindcss/postcss': {} },
}
```

`app/globals.css`:

```css
@import "tailwindcss";
```

## Config notes

- Tailwind v4 uses CSS-based config (`@theme` in `globals.css`) instead of `tailwind.config.js` — check which major version a copy-pasted component targets before dropping it in.
- Define your brand colors, font stacks, and custom easing curves once in `@theme`, then reference them everywhere — this is what keeps 40+ UI components looking like one cohesive design system instead of a bookmark collection.

```css
@theme {
  --font-display: "General Sans", sans-serif;
  --color-brand: oklch(62% 0.19 260);
  --ease-premium: cubic-bezier(0.16, 1, 0.3, 1);
}
```

## Common mistakes

- Mixing Tailwind v3 config syntax (`tailwind.config.js` with `theme.extend`) into a v4 project — the two config systems don't merge automatically.
- Not purging: in v4 this is automatic via content detection, but double check `@source` directives if components live outside the default scanned paths (e.g. a separate `packages/ui` workspace).

## Official links

- Docs: https://tailwindcss.com/docs
- GitHub: https://github.com/tailwindlabs/tailwindcss
