# Cleaning Rules

## What to remove

### Placeholder comments
Lines that are only HTML comments with no content — these are template noise:
```
<!-- patterns that consistently produce good output -->
<!-- recurring issues, edge cases -->
```
Remove if the section has no real entries below them.

### Duplicate entries
Two entries that describe the same observation — keep the more specific one, remove the other.

### Generic observations
Entries that could apply to any skill and teach nothing specific:
- "Be careful with edge cases"
- "Test before finalizing"
- "User prefers clear output"
Remove these — they carry no information.

### Stale entries
Entries that reference specific past behaviors that were fixed and no longer apply.
These are recognizable by past tense + resolved framing:
- "Used to produce X, fixed by doing Y" — if Y is now the default, remove.

---

## What to compress

### Verbose entries → one line
```
// Before
- When the user asks for a review, it's important to make sure that
  you check all the concurrency-related code carefully because goroutine
  leaks are easy to miss and the user cares a lot about them.

// After
- Always prioritize goroutine leak checks — user flags these most often.
```

### Near-duplicate entries → merge
Two entries about the same topic with slight variation → merge into one that covers both:
```
// Before
- Short responses work better
- User prefers concise output over detailed explanations

// After
- User prefers concise output — skip explanations unless asked.
```

---

## What to keep

Keep any entry that is:
- **Specific** — names a concrete pattern, file, behavior, or preference
- **Actionable** — tells the skill what to do differently next time
- **Non-obvious** — not already covered by the skill's core rules

```
// Keep — specific and actionable
- User rejects passive voice even in formal register — always rewrite to active.

// Remove — generic, already in core rules
- Make sure output is clear and well-structured.
```

---

## Section structure to preserve

Always output in this format, even after cleaning:

```markdown
# Learnings

## What works well
[entries or empty]

## What to watch for
[entries or empty]
```

Never collapse the two sections into one even if one is empty.
