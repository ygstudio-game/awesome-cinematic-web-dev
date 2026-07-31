# Playwright MCP

**What it is:** An MCP server that lets your AI agent (Claude Code, Cursor, etc.) control a real browser — navigate, click, read the DOM/accessibility tree, and take screenshots of your *running* app.

**Why use it:** Without it, the agent only ever sees source code — it can generate a Motion.dev reveal or R3F scene that's syntactically fine but visually broken (wrong easing, overlapping elements, canvas not rendering) and has no way to notice. With it, the agent can load `localhost:3000`, look at the actual result, and iterate.

**When to use it:** After generating any visual component — hero sections, scroll sequences, 3D scenes — have the agent open the page and verify before you do, and again as a pre-deploy QA pass (see the workflow diagram in `Resources.md`).

## Install

```bash
npm install -g @playwright/mcp
```

Register with Claude Code:

```bash
claude mcp add playwright -- npx @playwright/mcp@latest
```

Or add manually to your MCP config (`.claude/mcp.json` / Cursor's `mcp.json`):

```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": ["@playwright/mcp@latest"]
    }
  }
}
```

## Typical workflow

1. `npm run dev` in one terminal.
2. Ask the agent: "Open localhost:3000, screenshot the hero section, and check that the R3F canvas rendered without console errors."
3. Ask it to resize to a mobile viewport and re-check — catches responsive breakage before you do manually.

## Common mistakes

- Not having the dev server running before invoking the agent's browser tools — it'll hit a connection error.
- Treating a passing screenshot as proof of performance — Playwright MCP verifies visual/functional correctness, not Lighthouse scores; still run a real audit (`08-Optimization/Lighthouse.md`).

## Official links

- GitHub: https://github.com/microsoft/playwright-mcp
