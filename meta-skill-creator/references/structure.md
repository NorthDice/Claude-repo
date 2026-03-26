# SKILL.md Structure

Every `SKILL.md` follows this structure in order:

## 1. Frontmatter (required)

```yaml
---
name: skill-name
description: One sentence. Include: trigger words | exclusions | expected output.
---
```

Description formula:
> "[Action] [subject]. Trigger when [trigger words / situations]. Exclude when [anti-triggers]. Output: [what the user gets]."

## 2. Title + one-line purpose

```markdown
# Skill Name

One sentence: what this skill does and why.
```

## 3. Core Rules (required, always loaded)

Numbered list of non-negotiable constraints. Short — each rule fits in one line.

```markdown
## Core Rules

1. Rule one
2. Rule two
```

## 4. Workflow

Numbered steps. Each step = one action. If a step needs detail → link to a references file.

```markdown
## Workflow

1. **Step name** — what to do. See [detail.md](references/detail.md) if needed.
2. **Step name** — what to do.
```

## 5. Output Format (if applicable)

Show the exact format the skill should produce. Use a code block.

## What does NOT belong in SKILL.md

- Long examples (→ references file)
- Exhaustive checklists (→ references file)
- Background explanations (→ references file)
- Anything that doesn't change the workflow
