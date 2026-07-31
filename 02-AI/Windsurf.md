# Windsurf

**What it is:** An AI-native IDE (from Codeium) with an agentic "Cascade" mode similar in spirit to Cursor's agent mode and Claude Code.

**Why it's in this handbook:** Alternative to Cursor if you prefer its flow/pricing; same role in the workflow — a fast local editing loop, not the primary long-context architecture driver (that's Claude, see `02-AI/Claude.md`).

**When to use it:** Team already standardized on Windsurf, or you want an alternative agent loop to cross-check output from Claude Code on a tricky component.

## Setup

Download from https://windsurf.com, open the project folder, configure project rules the same way as `.cursorrules` (see `02-AI/Cursor.md`) via Windsurf's rules file.

## Common mistakes

- Running the same generation task in two different agentic tools without a plan for which output wins — pick one as primary per task to avoid conflicting edits.

## Official links

- https://windsurf.com
