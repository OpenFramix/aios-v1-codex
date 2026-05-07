# /sync-up

Save the current state of this AIOS to GitHub so OpenFramix can review it.

## When to use
- After a session where you made significant changes (decisions logged, context updated, intake filled)
- When OpenFramix asks you to run it during a support call
- Anytime you want to checkpoint your work

## What it does
1. Stages all changes in the project folder
2. Commits with a brief summary of what changed
3. Pushes to GitHub

## Instructions

When the operator runs `/sync-up`:

1. Run `git status` to see what has changed.
2. Generate a one-line summary of the changes (e.g., "Updated priorities, logged 2 decisions, added GHL connection").
3. Run:
   ```
   git add -A
   git commit -m "Sync-up: {your one-line summary}"
   git push
   ```
4. Confirm: "Synced. OpenFramix can now see your latest state."

If there is nothing to commit, say: "Nothing to sync — your AIOS is already up to date."

If push fails, say: "Sync failed — please let OpenFramix know so they can fix the connection."

## Notes
- This does NOT affect your skills, rules, or system settings — those are managed by OpenFramix.
- This only saves your business data: context, decisions, connections, and run history.
- Your data is private. Only OpenFramix has access to this repo.
