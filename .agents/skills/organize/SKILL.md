# /organize

Scan the AIOS folder, identify anything out of place, move it to the right location, and update the canonical folder structure reference. Keeps the system clean without breaking any connections.

## When to use
- After onboarding, to make sure everything landed in the right place
- After any session where new files were created or downloaded
- Anytime the folder feels messy or hard to navigate
- Before running /sync-up so what gets pushed is clean

## What it does
1. Reads `references/folder-structure.md` to understand the canonical layout
2. Scans the full project folder for misplaced files
3. Moves anything that belongs in a different folder
4. Checks for any new folders that appeared and documents them
5. Updates `references/folder-structure.md` with the current state
6. Reports a summary of what moved and what's clean

## What it never touches
These are load-bearing system files. Never move, rename, or delete them:
- `AGENTS.md`, `EXPANSIONS.md`, `INSTALL.md`, `README.md`, `VERSION.md`
- `aios-intake.md`, `connections.md`, `.gitignore`
- Anything inside `.agents/` (skills, rules) — managed by OpenFramix
- Core context files: `context/about-business.md`, `context/about-me.md`, `context/candidates.md`, `context/domains.md`, `context/priorities.md`, `context/tech-stack.md`
- `decisions/log.md`
- Anything inside `references/` (except updating `folder-structure.md`)

## Instructions

When the operator runs `/organize`:

### Step 1 — Read the canonical structure
Read `references/folder-structure.md` to understand where things belong.

### Step 2 — Scan for misplaced files
Check these locations for files that don't belong:

**Root directory:** Look for any files that are not in the "What never moves" list above.
- Files matching `audit-*.md` or `*-audit-*.md` → move to `audits/`
- Files matching `morning-brief-*.md` → move to `runs/`
- Files matching `session-summary-*.md` → move to `runs/`
- Files matching `level-up-*.md` → move to `runs/`
- Files matching `roi-report-*.md` → move to `runs/`
- Files matching `explore-*.md` → move to `runs/`
- Files matching `*.png`, `*.jpg`, `*.jpeg`, `*.svg`, `*.pdf`, `*.gif` → move to `brand-assets/` (create if needed)
- Files matching `*.mp4`, `*.mov`, `*.avi` → move to `brand-assets/video/` (create if needed)
- Any other loose files that don't match known root files → move to `archives/YYYY-MM-DD/`

**`runs/` directory:** Look for files that don't match the expected naming patterns. Move anything clearly out of place to `archives/`.

**`audits/` directory:** Same — anything that isn't an audit report goes to `archives/`.

**`tracking/` and `archives/`:** These are flexible — leave them alone unless there are obvious naming collisions.

### Step 3 — Execute moves
Move the files identified in Step 2. Create destination folders if they don't exist.

Before moving any file, verify it is not referenced by name in `AGENTS.md`, `connections.md`, or any skill file. If it is referenced, flag it instead of moving it.

### Step 4 — Check for new folders
Compare the current folder list against `references/folder-structure.md`. If any new folders exist that aren't documented:
- Add them to the appropriate section in `folder-structure.md`
- Note what they contain

### Step 5 — Update `references/folder-structure.md`
Update the `Last organized:` timestamp at the top of the file to today's date.
Update the folder tree if anything changed (new folders added, old ones removed).

### Step 6 — Report

Print a summary:

```
/organize — YYYY-MM-DD

Moved:
  - {filename} → {destination}     (reason)
  - (or "Nothing to move — already clean.")

Flagged (referenced, not moved):
  - {filename}: referenced in {file} — review manually

New folders documented:
  - {folder-name}: {brief description}

Folder structure reference updated: references/folder-structure.md
```

## Notes
- `/organize` does NOT run `/sync-up`. If you want to push the organized state to GitHub, run `/sync-up` separately after.
- If unsure whether to move something, flag it instead of moving it. Better to ask than to break a connection.
- If a destination folder doesn't exist, create it with a `.gitkeep` file so it's tracked.
- Never delete files — only move them. If something looks like it should be deleted, flag it for the operator.
