# Skills: 7 Rules

## Rule 1 — What a skill is

A skill is a folder of knowledge. Its "brain" is `SKILL.md` — a standard operating procedure (SOP) that tells the AI what to do and how.

**Progressive Disclosure** is the key principle: don't load everything at once. `SKILL.md` contains only the core instructions; detailed content is pulled from additional files only when needed at a specific step.

```
skills/
  my-skill/
    SKILL.md          ← core instructions (max 200 lines)
    references/
      brand-voice.md  ← loaded only at the copywriting step
      audience.md     ← loaded only at the targeting step
```

---

## Rule 2 — Context optimization (200-line rule)

> **⚠️ The main mistake:** One giant `SKILL.md` at 1000 lines — the AI starts to slow down and ignore instructions.

**Golden rule:** `SKILL.md` must not exceed **200 lines**. It serves as a table of contents; details live in separate files of 200–300 lines each.

The skill description must include:
- **Trigger words** — when to run
- **Exclusions** — when not to run
- **Expected output** — what the result should be

> **Example description:**
> ```
> Trigger: when user asks to write a LinkedIn post
> Exclude: technical texts, internal documentation
> Output: 150–200 word post in brand tone of voice
> ```

---

## Rule 3 — Refactoring existing skills

Skills from open repositories are often a 1000-line wall of text with no structure.

**Fix:** split the blob:
- core logic → `SKILL.md`
- knowledge base → `references/` folder

> **Result:** up to 60% fewer tokens loaded without losing quality. Instead of loading 1000 lines every time — only the relevant chunk.

```
Before: SKILL.md (1000 lines) — loaded in full every time

After:
  SKILL.md           (150 lines) — always loaded
  references/
    rules.md         (300 lines) — loaded only at validation step
    examples.md      (250 lines) — loaded only at generation step
```

---

## Rule 4 — Business context

A skill without context produces generic output. The AI writes "like a typical AI".

**What to add to `references/`:**

| File | Contents |
|------|----------|
| `brand-voice.md` | Tone, style, forbidden words |
| `audience.md` | Target audience profile, pain points, language |
| `positioning.md` | USP, competitors, key differentiators |

> **Without context:** "Our product helps you achieve your goals effectively."
>
> **With context:** "Forget the Excel spreadsheets — automate the routine in 10 minutes."

---

## Rule 5 — Evals

Evaluating results "by eye" is ineffective. Evals let you test skills against concrete metrics.

**A/B test:** run a task with a reference file and without it → check whether the file actually improves the result or just wastes tokens.

> **Example metrics for a copywriting skill:**
> - Matches tone of voice: 1–5
> - Has CTA: yes/no
> - Within length limits: yes/no
> - No AI clichés (effective, innovative, leverage): yes/no

---

## Rule 6 — Self-improvement

A skill should get better after each use.

**Mechanism:** `learnings.md` with a feedback loop.

```markdown
## What works well
- Adding industry examples increases relevance
- Short paragraphs work better in this format

## What to watch for
- Formal tone gets rejected by the user
- Lists of 5+ items → user asks to shorten
```

> **⚠️ Important:** Clean `learnings.md` periodically — otherwise it becomes a source of context bloat itself.

---

## Rule 7 — AI team (interconnected system)

At the highest level, skills stop working in isolation. They form an operating system — calling each other.

```
copywriting-skill
  → humanizer-skill      ← removes robotic style
  → repurpose-skill      ← reformats for other channels
  → eval-skill           ← scores result against metrics
```

All skills share a **common business context** (brand voice, audience, positioning) and work as a coordinated system — an AI workforce.

> **Bottom line:** A skill system is not a toolbox. It's a team where each member knows their role and hands work off to the next.
