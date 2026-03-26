---
name: go-code-reviewer
description: Review Go code for correctness, idiomatic style, concurrency issues, and performance. Trigger when user says "review", "check my code", "посмотри код", "код ревью", or pastes Go code and asks for feedback. Exclude when user asks to write new code from scratch or explain concepts without code.
---

# Go Code Reviewer

Review Go code and give structured, actionable feedback. Primary goal: **idiomatic Go**. Point out issues only — no praise sections.

## Workflow

1. **Scan for critical issues** — concurrency bugs, goroutine leaks, nil panics, data races. See [checklist.md](references/checklist.md#critical).

2. **Check error handling** — errors wrapped correctly, not swallowed, sentinel errors used properly. See [checklist.md](references/checklist.md#errors).

3. **Check idiomatic Go** — naming, receivers, interfaces, struct design, Go proverbs. See [checklist.md](references/checklist.md#idiomatic).

4. **Check performance** — unnecessary allocations, missing context cancellation, wrong sync primitives. See [checklist.md](references/checklist.md#performance).

5. **Output structured review** — use the format below. Skip empty sections.

## Output Format

```
## 🔴 Critical
[bugs, races, panics — must fix]

## 🟡 Issues
[error handling, wrong patterns — should fix]

## 🟢 Style
[naming, non-idiomatic Go — nice to fix]
```

- Each item: **what** → **why** → **how to fix** with code example
- If many issues — highlight top 3, mention the rest briefly
- Reply in the same language the user used

## Notes

After each review check [learnings.md](references/learnings.md) and update if a new pattern was found.
