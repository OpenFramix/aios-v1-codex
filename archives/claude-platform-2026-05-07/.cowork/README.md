# .cowork/ — Cowork Delivery Layer

Environment-specific configuration for Claude Cowork delivery. Everything in this folder is Cowork-only. The 95% of the AIOS (skills, rules, context, references) lives outside this folder and is shared across both delivery modes.

## What goes here

- **Plugin bundle** — when built, the `.plugin` file (or equivalent Cowork format) that registers all AIOS skills as native slash commands in Cowork's command palette. Until the plugin is built, the CLAUDE.md skill triggers section handles slash command routing.
- **Connector config** — Cowork-specific OAuth connector setup notes, if any differ from the standard connections.md wiring.
- **Scheduled task definitions** — Cowork's native scheduled task format for automating `/morning-brief` and other recurring skills.

## Current status

Plugin not yet built. Skills execute via CLAUDE.md trigger fallback.

**Next step:** Use Cowork's built-in Plugin Creator to bundle `/morning-brief`, `/audit`, `/level-up`, `/explore`, `/roi-report`, and `/onboard` as native slash commands. Save the output here.

## Cowork-specific install steps

See `INSTALL.md → Mode B: Cowork` for the full Cowork setup sequence.
