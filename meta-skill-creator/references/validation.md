# Validation Checklist

Run after creating or refactoring any skill.

## SKILL.md

- [ ] Line count ≤ 200
- [ ] Frontmatter has `name` and `description`
- [ ] Description includes: trigger | exclusions | output
- [ ] Has `## Core Rules` section
- [ ] Has `## Workflow` with numbered steps
- [ ] No long examples or checklists inline — extracted to references
- [ ] Every reference link points to an existing file

## References

- [ ] Every file has a self-describing name
- [ ] No file exceeds 300 lines
- [ ] `learnings.md` exists
- [ ] `rules.md` exists and is initially empty
- [ ] No file named `extra`, `misc`, `details`, `ref`, or similar

## Formulations

- [ ] No vague steps like "review the code" → should be "check X for Y, flag if Z"
- [ ] Each workflow step = one concrete action
- [ ] Output format is shown as an example, not described in prose

## Quick fix guide

| Issue | Fix |
|-------|-----|
| SKILL.md > 200 lines | Extract longest sections to references/ |
| Vague step | Add: what to look for + what to do when found |
| Missing reference file | Create with self-describing name |
| Generic reference link | Move link to the specific step that needs it |
| No learnings.md | Create from template in required-files.md |
| No rules.md | Create empty from template in required-files.md |
