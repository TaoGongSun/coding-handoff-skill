# coding-handoff-skill

A minimal handoff skill for coding agents. When work must move to another session, model, or agent, it creates one new Markdown file describing the grounded current state and the immediate next step.

It is intentionally not a task tracker or state-management system.

## Behavior

- Stores handoffs under `<project-root>/.ai/handoffs/`.
- Creates a new timestamped Markdown file every time and never overwrites an older handoff.
- Allows any Markdown sections in any order.
- Records only facts supported by the conversation or repository.
- Points to repository files instead of copying large source files or documents.
- Treats Git details as ordinary context, not handoff validity metadata.
- Resumes by reading the selected or newest relevant handoff, checking the current repository, and continuing from the immediate next step.

It has no CLI, daemon, hook, database, ownership model, lifecycle, registry, generated index, or schema validator.

## Install

The skill directory contains `SKILL.md` and `LICENSE`. Copy or symlink the directory as `handoff` in the user skill location used by the agent:

- Codex: `~/.agents/skills/handoff`
- Claude Code: `~/.claude/skills/handoff`
- Antigravity CLI (`agy`): `~/.gemini/config/skills/handoff`

## Use

- Codex: mention `$handoff`, or ask to hand off work to another session or model.
- Claude Code: use `/handoff`, or ask for a handoff.
- Agy: use `/handoff`, or ask for a handoff.

Example:

```text
$handoff Leave a handoff for the next session.
```

To resume, name the handoff file when possible:

```text
Resume from .ai/handoffs/2026-08-28-0200-parser-review.md.
```

If no file is named, the agent lists `.ai/handoffs/` and selects the most relevant, then newest, document.

## Output

```text
.ai/handoffs/YYYY-MM-DD-HHMM-short-topic.md
```

If that filename exists, the agent uses `-2`, `-3`, and so on. Existing handoffs remain unchanged.

## Origin and license

Adapted from [ToolMonsters/handoff-skill](https://github.com/ToolMonsters/handoff-skill), created by Yonathan Cohen (Tool Monsters). The original project and this adaptation are distributed under the MIT License. See [LICENSE](./LICENSE).
