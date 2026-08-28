---
name: handoff
description: Create, refresh, or resume a compact coding handoff when the user asks for a handoff, 交接, resume, another session or model, or work must genuinely stop at a context, quota, or session boundary. Do not use merely because work is large, planned, multi-file, or involves Git, and do not use when the current run can finish the work.
---

# Handoff

Maintain one portable Markdown snapshot of the current work so another coding agent can continue without a state-management system or a growing history log.

## Create or refresh a handoff

1. Use the repository root as the project root. If there is no repository, use the current project root. The target must come from the host agent's active workspace or an explicit user path. If neither exists, ask the user to select or attach a project; do not silently write into a host-managed scratch directory.
2. Use `.ai/HANDOFF.md` as the single active handoff. It is a replaceable working snapshot, not an append-only record, index, registry, database, lock, ownership record, or lifecycle state file.
3. Before writing, read the existing `.ai/HANDOFF.md` and any legacy `.ai/handoffs/*.md`, then inspect relevant project files and Git state. Treat the current project as authoritative. Gather only supported facts, and label uncertainty instead of guessing.
4. Rewrite `.ai/HANDOFF.md` as a compact statement of what is true and actionable now. Do not append a chronological update. Retain a paragraph only when removing it could cause the next agent to act incorrectly or lose information that is not reliably stored elsewhere.
5. Use ordinary Markdown with whichever sections and order best preserve the current work. Useful sections, when applicable, include:

   - Goal / Context
   - Current state
   - Important decisions
   - Verification
   - Remaining
   - Immediate next step
   - Constraints / pitfalls
   - Relevant files
   - Unstored drafts, patches, commands, or exact text needed to continue

   Omit empty sections. Preserve useful custom sections and their order, but remove completed history, superseded decisions or verification, stale next steps, and failed attempts that no longer affect the remaining work.
6. Prefer exact repository pointers over duplication. When work is reliably stored in the repository, record the precise path, modification status, and useful branch, commit, or diff context. Do not copy large source files or documents into the handoff. Include content verbatim only when it is not reliably stored elsewhere and the next agent truly needs the exact text.
7. Treat Git information as optional context, never as validity metadata. Reconcile it with the current project on every refresh instead of preserving stale Git details.
8. After writing, reread `.ai/HANDOFF.md` and confirm that it contains the still-relevant information and a usable next step. Only then delete superseded Markdown handoffs under `.ai/handoffs/` and remove that directory if it becomes empty. A handoff request authorizes this cleanup of handoff artifacts, but does not authorize changes to plans, source files, branches, commits, or Git configuration.
9. Keep multiple active handoff files only when the user explicitly requests separate parallel workstreams. Give each workstream one stable, non-timestamped filename and refresh it by the same replacement rules.
10. Report the active handoff path and any obsolete handoff files removed. State whether removed files remain recoverable through Git. Do not claim the work itself is complete unless verification supports that claim.

Never put secrets, tokens, credentials, or unnecessary private data in a handoff.

## Resume from a handoff

1. If the user names a handoff, read that exact file. Otherwise read `.ai/HANDOFF.md`. If it does not exist, inspect legacy `.ai/handoffs/*.md` and choose the most relevant handoff, using the newest timestamp when relevance is equal.
2. Read the handoff, then inspect its referenced project files and current Git state only as needed.
3. Treat the current project as authoritative. If it differs from the handoff, state the difference and do not assume either side explains the other.
4. Continue from `Immediate next step`, or the clearest remaining action if that heading is absent. Stop for user input only when the current state makes the recorded step unsafe, obsolete, or materially ambiguous.
5. Do not claim, reclaim, lock, register, rewrite, move, or delete anything merely to resume. If the continued work later needs another handoff, refresh the active snapshot and remove information that has become obsolete.

## Origin

Adapted from [ToolMonsters/handoff-skill](https://github.com/ToolMonsters/handoff-skill), created by Yonathan Cohen (Tool Monsters) and distributed under the MIT License. This version retains the portable Markdown handoff and zero-invention principles, with a repository-oriented rolling snapshot and a lightweight resume workflow.
