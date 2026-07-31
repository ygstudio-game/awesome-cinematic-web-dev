# MagicUI MCP

**What it is:** An MCP server exposing MagicUI's component library directly to your AI agent — so it can browse available components and pull real, current source instead of guessing/hallucinating a component's API from memory.

**Why use it:** Static training knowledge of a UI library goes stale and can hallucinate props that don't exist. The MCP server gives the agent live access to the actual component source and demo usage.

## Install

Register with Claude Code / Cursor per MagicUI's MCP documentation (server name and exact package may change — check https://magicui.design for current install command). Typical pattern:

```bash
claude mcp add magicui -- npx @magicui/mcp@latest
```

## Typical workflow

> "Using the MagicUI MCP, find a component suited for an animated pricing table and install it into `components/ui/`."

The agent lists available components, shows you the match, and can scaffold it directly via MagicUI's CLI (`npx shadcn add <magicui-registry-url>`).

## Common mistakes

- Hand-writing a MagicUI-style component from memory instead of pulling the real one via MCP — you lose the maintenance/update path and likely reintroduce a bug MagicUI already fixed upstream.

## Official links

- https://magicui.design
