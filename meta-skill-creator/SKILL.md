---
name: meta-skill-creator
description: Create and refactor Claude Code skills. Trigger when user asks to create a new skill, edit an existing skill, or says a skill is too long / unclear / bloated. Exclude when user asks to use a skill, not modify it.
---

# Meta Skill Creator

Create and refactor skills so they are focused, fast to load, and easy to extend.

## Core Rules

1. `SKILL.md` must never exceed **200 lines** — it's a SOP, not a knowledge base
2. Every file in `references/` must be self-describing by name alone
3. Every skill must have `references/learnings.md` and `references/rules.md`
4. Vague or scattered instructions → group into clear steps
5. The description field must include: trigger words, exclusions, and expected output

## Workflow

### Creating a new skill

1. **Clarify scope** — ask: what triggers this skill, what does it output, what should it never do
2. **Write `SKILL.md`** — SOP only: trigger, workflow steps, output format. See [structure.md](references/structure.md)
3. **Extract knowledge** — anything longer than a short example goes into `references/`. See [references-guide.md](references/references-guide.md)
4. **Add required files** — `learnings.md` and `rules.md`. See [required-files.md](references/required-files.md)
5. **Validate** — check against [validation.md](references/validation.md)

### Refactoring an existing skill

1. **Read the skill** — measure line count, identify bloated sections
2. **Check SKILL.md size** — if > 200 lines: extract reference content into `references/` with self-describing names
3. **Sharpen formulations** — vague phrases → concrete rules with examples
4. **Check required files** — add `learnings.md` and `rules.md` if missing
5. **Validate** — check against [validation.md](references/validation.md)

## Skill Directory Structure

```
~/.claude/skills/skill-name/
  SKILL.md              ← SOP only, max 200 lines
  references/
    [topic].md          ← self-describing names, loaded on demand
    learnings.md        ← feedback loop, updated after each use
    rules.md            ← user-defined hard rules, always loaded
```
