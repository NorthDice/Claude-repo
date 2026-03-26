# References Guide

## When to extract to a references file

Extract when:
- A section is longer than ~20 lines
- Content is reference material, not a workflow step
- Content is only needed at a specific step (not always)
- It's a checklist, example set, or lookup table

Keep in SKILL.md:
- Workflow steps (even if they reference external files)
- Core Rules
- Output format template

## Naming rules

File names must be self-describing — a developer reading only the filename should know what's inside.

| Bad name | Good name |
|----------|-----------|
| `extra.md` | `error-handling.md` |
| `ref1.md` | `goroutines.md` |
| `details.md` | `output-format-examples.md` |
| `misc.md` | `naming-conventions.md` |

## How to reference from SKILL.md

Link at the relevant workflow step, not as a generic "see also":

```markdown
// BAD — generic, not actionable
See references/ for more details.

// GOOD — linked at the step where it's needed
2. **Check error handling** — wrap with %w, check for nil-interface trap.
   See [error-handling.md](references/error-handling.md).
```

## File size

Each references file should stay under 300 lines. If a topic grows beyond that — split by subtopic:

```
error-handling.md          → wrapping, sentinel errors, early return
error-handling-patterns.md → complex multi-error, error groups
```
