# .claudecode/ — Claude Code Delivery Layer

Environment-specific configuration for Claude Code delivery. Everything in this folder is Code-only. The 95% of the AIOS (skills, rules, context, references) lives outside this folder and is shared across both delivery modes.

## What goes here

- **settings.json** — MCP server connections, tool permissions, hook configurations for Claude Code. Copy `settings.json.example` to `.claude/settings.json` during setup and fill in the client's credentials.
- **Routines** — Claude Code scheduled task definitions (if using Claude Code Routines for `/morning-brief` automation rather than a cron job).

## Current status

See `settings.json.example` for the recommended starting configuration.

## Claude Code-specific install steps

See `INSTALL.md → Mode A: Claude Code` for the full Code setup sequence.
