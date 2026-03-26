---
name: learnings-cleaner
description: Clean and compress learnings.md files across all skills. Trigger when user says "почисти learnings", "clean learnings", "сожми learnings", or explicitly invokes this skill. Never runs automatically — only on direct call.
---

# Learnings Cleaner

Scan all skills, read their `learnings.md`, and compress them — remove noise, merge duplicates, keep only concrete actionable observations.

## Core Rules

1. Never delete entries that contain a specific, concrete observation
2. Never touch `rules.md` — only `learnings.md`
3. Keep the two-section structure: `## What works well` / `## What to watch for`
4. If a file is empty or has only placeholder comments — leave it as-is
5. Report every change made — don't silently overwrite

## Workflow

1. **Find all skills** — list all directories in `~/.claude/skills/`

2. **Read each learnings.md** — path: `~/.claude/skills/<skill>/references/learnings.md`
   Skip if file doesn't exist or contains only placeholder comments.

3. **Clean each file** — apply rules from [cleaning-rules.md](references/cleaning-rules.md)

4. **Write back** — overwrite only if content actually changed

5. **Report** — for each skill: what was removed / merged / kept. See output format below.

## Output Format

```
## Learnings cleanup report

### skill-name
- Removed: [what and why]
- Merged: [what was combined]
- Kept: [count] entries
- No changes / Skipped (empty)

### skill-name
...
```

If nothing needed cleaning: "All learnings.md files are clean."
