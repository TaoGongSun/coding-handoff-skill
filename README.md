# coding-handoff-skill

A minimal handoff skill for coding agents. When work must move to another session, model, or agent, it refreshes one compact Markdown file describing the grounded current state and the immediate next step.

It is intentionally not a task tracker or state-management system.

## Behavior

- Stores the active handoff at `<project-root>/.ai/HANDOFF.md`.
- Rewrites the active handoff as a current-state snapshot instead of appending history.
- Removes completed, superseded, and otherwise obsolete handoff content on every refresh.
- Consolidates and removes legacy timestamped files under `.ai/handoffs/` after the replacement has been verified.
- Allows any Markdown sections in any order.
- Records only facts supported by the conversation or repository.
- Points to repository files instead of copying large source files or documents.
- Treats Git details as ordinary context, not handoff validity metadata.
- Resumes by reading the active handoff, checking the current repository, and continuing from the immediate next step.

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

For non-interactive Agy runs, attach the repository explicitly when no Agy project is already active, for example:

```sh
agy --add-dir /absolute/path/to/repository -p "/handoff Leave a handoff for the next session."
```

Without an active or attached project, the skill asks for a repository instead of treating Agy's managed scratch directory as the project.

Example:

```text
$handoff Leave a handoff for the next session.
```

To resume, name the handoff file when useful:

```text
Resume from .ai/HANDOFF.md.
```

If no file is named, the agent reads `.ai/HANDOFF.md`. Legacy `.ai/handoffs/*.md` files are used only as a migration fallback.

## Output

```text
.ai/HANDOFF.md
```

Each handoff refresh replaces obsolete information in this file. After the replacement is reread and verified, superseded legacy handoff files are removed. Multiple stable handoff files are allowed only when the user explicitly requests parallel workstreams.

## Origin and license

Adapted from [ToolMonsters/handoff-skill](https://github.com/ToolMonsters/handoff-skill), created by Yonathan Cohen (Tool Monsters). The original project and this adaptation are distributed under the MIT License. See [LICENSE](./LICENSE).
