# shadcn MCP

**What it is:** An MCP server for shadcn/ui's component registry — the agent can browse, add, and customize components directly, including third-party registries built on shadcn's CLI (MagicUI, Aceternity, and others distribute through the same registry mechanism).

**Why use it:** shadcn components are copy-into-your-repo, not an installed dependency — meaning your agent needs to actually fetch current source rather than recall it. MCP access keeps that fetch grounded in the real, current registry.

## Install

```bash
claude mcp add shadcn -- npx shadcn@latest mcp
```

## Typical workflow

> "Use the shadcn MCP to add a dialog component and adapt it to our Tailwind theme variables from `01-Setup/Tailwind.md`."

Since MagicUI, Aceternity, and 21st.dev all publish through shadcn-compatible registries, this MCP server is often the single integration point for pulling components from all of `04-UI/`.

```bash
npx shadcn@latest add <component-registry-url>
```

## Common mistakes

- Adding a component then never customizing the copied source to match your theme tokens — defeats the point of "copy into your repo," which is that you're supposed to own and adapt it.

## Official links

- https://ui.shadcn.com
