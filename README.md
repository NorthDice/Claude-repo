# Claude-repo

A curated collection of Claude Code agents, skills, and workflow configurations designed for Go development and general software engineering tasks.

## What's in here

### Agents (`.claude/agents/`)

Specialized subagents that Claude Code can spawn to handle focused tasks:

| Agent | Model | Purpose |
|-------|-------|---------|
| `system-architect` | Opus | Designs minimal, justified system architectures. No over-engineering. |
| `go-code-reviewer` | Sonnet | Reviews Go code for correctness, memory safety, performance, and idiomatic patterns. |
| `grill-me` | Sonnet | Interrogates developers on their changes before merging — earn your merge. |
| `code-simplifier` | Opus | Strips unnecessary complexity from code without changing behavior. |
| `claude-skill-builder` | Sonnet | Builds new Claude skill files from developer intent. |

### Skills (`.claude/skills/`)

Reusable Claude behaviors invoked via slash commands:

| Skill | Trigger | Purpose |
|-------|---------|---------|
| `unit-test-writer` | `/unit-test-writer` | Generates comprehensive, table-driven Go unit tests. |

### Workflow Configuration (`CLAUDE.md`)

Project-level instructions that govern Claude's behavior:

- **Plan-first** — enters plan mode for any non-trivial task
- **Subagent strategy** — offloads research and parallel work to keep context clean
- **Self-improvement loop** — captures lessons from corrections in `tasks/lessons.md`
- **Verification gate** — never marks tasks complete without proving correctness
- **Autonomous bug fixing** — resolves issues from logs/errors without hand-holding

## Usage

Clone this repo and copy the `.claude/` directory into your project:

```bash
git clone <repo-url>
cp -r Claude-repo/.claude /your/project/
cp Claude-repo/CLAUDE.md /your/project/
```

Or reference individual agent/skill files as needed.

## Agent Persistent Memory

Each agent has its own memory directory at `.claude/agent-memory/<agent-name>/`. Memory persists across sessions and is shared via version control, building institutional knowledge about the codebase over time.
