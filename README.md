# coding-handoff-skill

A minimal handoff skill for coding agents. When work must move to another session, model, or agent, it refreshes a compact Markdown snapshot for that workstream describing the grounded current state and the immediate next step.

It is intentionally not a task tracker or state-management system.

## Behavior

- Preserves the project's existing handoff convention.
- Supports `.ai/HANDOFF.md` as either a standalone handoff or an index of independent workstreams.
- Keeps one maintained snapshot per workstream and rewrites that file instead of appending history.
- Removes completed, superseded, and otherwise obsolete handoff content on every refresh.
- Updates only the current workstream's index entry when an index exists.
- Never bulk-deletes `.ai/handoffs/` or touches unrelated workstreams.
- Removes an old file only when it demonstrably belongs to the same workstream and is fully superseded.
- Allows any Markdown sections in any order.
- Records only facts supported by the conversation or repository.
- Points to repository files instead of copying large source files or documents.
- Treats Git details as ordinary context, not handoff validity metadata.
- Resumes by selecting the relevant workstream from the project handoff or index, checking the current repository, and continuing from the immediate next step.

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

To resume, name the workstream handoff when useful:

```text
Resume from .ai/handoffs/parser-review.md.
```

If no file is named, the agent first determines whether `.ai/HANDOFF.md` is a standalone handoff or an index, then selects the workstream most relevant to the current conversation.

## Output

```text
.ai/HANDOFF.md
# or, when the project uses an index or multiple workstreams:
.ai/handoffs/<short-topic>.md
```

Each refresh rewrites only the selected workstream's handoff and, when needed, its own index entry. Existing unrelated handoffs are preserved. A same-workstream predecessor may be removed only after the replacement is verified and the old file is no longer referenced.

## Origin and license

Adapted from [ToolMonsters/handoff-skill](https://github.com/ToolMonsters/handoff-skill), created by Yonathan Cohen (Tool Monsters). The original project and this adaptation are distributed under the MIT License. See [LICENSE](./LICENSE).
