# ReactBits MCP

**What it is:** An MCP server exposing ReactBits' animated component collection (backgrounds, text effects, buttons) to your agent for live lookup and install.

**Why use it:** Same rationale as MagicUI MCP — ReactBits ships many small, highly specific animated components (text scramble, particle backgrounds, magnetic buttons); an agent with live registry access picks the right one and gets current source instead of reinventing a rough approximation.

## Install

```bash
claude mcp add reactbits -- npx reactbits-mcp@latest
```
(Verify current package name at https://reactbits.dev — MCP tooling here is newer and names shift.)

## Typical workflow

> "Using the ReactBits MCP, find an animated text-reveal component for the hero headline and wire it into our Motion.dev-based reveal pattern."

## Common mistakes

- Pulling a ReactBits component that uses GSAP internally into a project that's standardized on Motion.dev per `01-Setup/GSAP.md` — check the component's dependencies before adding it, or you end up running two animation engines.

## Official links

- https://reactbits.dev
