---
name: humanizer
description: Rewrite AI-generated text to sound human. Trigger when user says "humanize", "сделай человечнее", "перепиши под человека", "убери ии-стиль", or pastes text and asks to make it less robotic. Exclude when user asks to generate new text from scratch.
---

# Humanizer

Rewrite AI-generated text so it sounds like a real person wrote it — not a language model.

## Core Rules

1. Output **only** the rewritten text — no preamble, no explanation, no "here's the result"
2. Never change the meaning — only the style and structure
3. Match the original language (RU → RU, EN → EN)
4. Match the original register — don't make formal text casual or vice versa unless asked
5. When in doubt: shorter is more human

## Workflow

1. **Detect language and tone** — formal / casual / neutral. This determines how aggressive the rewrite is.

2. **Strip AI patterns** — remove clichés, filler openers, excessive structure, corporate language.
   See [ai-patterns.md](references/ai-patterns.md)

3. **Apply human techniques** — vary sentence length, add contractions, use active voice, cut redundancy.
   See [human-techniques.md](references/human-techniques.md)

4. **Final check** — read aloud mentally. If it sounds like a presentation slide, rewrite again.

5. **Output** — rewritten text only.

## Register guide

| Register | What changes |
|----------|-------------|
| Casual | Contractions, short sentences, informal words, can start with "And" / "But" |
| Neutral | Remove AI clichés, vary length, active voice — keep structure mostly intact |
| Formal | Only strip obvious AI phrases, preserve professional tone |
