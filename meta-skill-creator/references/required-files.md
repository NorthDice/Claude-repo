# Required Files in Every Skill

Every skill must have these two files in `references/`:

---

## learnings.md

Feedback loop — updated after each skill use. Tracks what works and what doesn't.

Template:
```markdown
# Learnings

## What works well
<!-- patterns that consistently produce good output -->

## What to watch for
<!-- recurring issues, edge cases -->
```

Rules:
- Update after each session if a new pattern was found
- Keep entries short — one line per observation
- Prune regularly — if file grows > 50 lines, remove outdated entries

---

## rules.md

Hard rules set by the user. Always loaded with SKILL.md. Initially empty.

Template:
```markdown
# Rules

<!-- User-defined rules that override default skill behavior -->
<!-- Add rules here as you discover what works for your workflow -->
```

Rules:
- Never pre-populate with assumptions
- Only the user adds rules here — the skill never auto-writes to this file
- Rules here take priority over everything else in the skill
