---
name: handoff
description: Create, refresh, or resume a compact per-workstream coding handoff when the user asks for a handoff, 交接, resume, another session or model, or work must genuinely stop at a context, quota, or session boundary. Do not use merely because work is large, planned, multi-file, or involves Git, and do not use when the current run can finish the work.
---

# Handoff

Maintain a portable Markdown snapshot for the current workstream so another coding agent can continue without a state-management system or a growing history log.

## Create or refresh a handoff

1. Use the repository root as the project root. If there is no repository, use the current project root. The target must come from the host agent's active workspace or an explicit user path. If neither exists, ask the user to select or attach a project; do not silently write into a host-managed scratch directory.
2. Before choosing a file, inspect `.ai/HANDOFF.md`, `.ai/handoffs/*.md`, and relevant project instructions when they exist. Determine whether `.ai/HANDOFF.md` is a standalone handoff or an index, and preserve the project's existing convention. Multiple workstreams already present in the project do not need fresh user authorization.
3. Select only the current workstream's handoff:

   - If the user names a file, use that exact file.
   - If an index links the current workstream, use the linked file.
   - If `.ai/HANDOFF.md` is a standalone handoff for the current workstream, use it.
   - If the project uses an index or already has multiple workstreams and the current workstream has no file, create one stable, non-timestamped `.ai/handoffs/<short-topic>.md` and add only its index entry.
   - If no handoff convention exists, use `.ai/HANDOFF.md` as a standalone handoff.

   Do not rename an existing workstream file merely to normalize its name.
4. Read the selected handoff, then inspect relevant project files and Git state. Treat the current project as authoritative. Gather only supported facts, and label uncertainty instead of guessing.
5. Rewrite the selected handoff as a compact statement of what is true and actionable now. Do not append a chronological update. Retain a paragraph only when removing it could cause the next agent to act incorrectly or lose information that is not reliably stored elsewhere.
6. Use ordinary Markdown with whichever sections and order best preserve the current work. Useful sections, when applicable, include:

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
7. Prefer exact repository pointers over duplication. When work is reliably stored in the repository, record the precise path, modification status, and useful branch, commit, or diff context. Do not copy large source files or documents into the handoff. Include content verbatim only when it is not reliably stored elsewhere and the next agent truly needs the exact text.
8. Treat Git information as optional context, never as validity metadata. Reconcile it with the current project on every refresh instead of preserving stale Git details.
9. After writing, reread the selected handoff and confirm that it contains the still-relevant information and a usable next step. If `.ai/HANDOFF.md` is an index, add or update only the current workstream's entry and preserve every unrelated entry.
10. Cleanup is scoped to the current workstream. Remove obsolete content inside its selected handoff. Delete another handoff file only when evidence shows that it belongs to the same workstream, the selected handoff fully supersedes it, and no index still references it. Never bulk-delete `.ai/handoffs/`, never delete an unrelated workstream, and leave ambiguous files untouched.
11. A handoff request authorizes changes only to the selected handoff, its own index entry when applicable, and clearly superseded files from the same workstream. It does not authorize changes to other handoffs, plans, source files, branches, commits, or Git configuration.
12. Report the selected handoff path, any index entry changed, and any same-workstream file removed. State whether removed files remain recoverable through Git. Do not claim the work itself is complete unless verification supports that claim.

Never put secrets, tokens, credentials, or unnecessary private data in a handoff.

## Resume from a handoff

1. If the user names a handoff, read that exact file. Otherwise inspect `.ai/HANDOFF.md` to determine whether it is a standalone handoff or an index. If it is an index, follow the entry most relevant to the current conversation; inspect `.ai/handoffs/*.md` only as needed. Use recency only when relevance is equal.
2. Read the handoff, then inspect its referenced project files and current Git state only as needed.
3. Treat the current project as authoritative. If it differs from the handoff, state the difference and do not assume either side explains the other.
4. Continue from `Immediate next step`, or the clearest remaining action if that heading is absent. Stop for user input only when the current state makes the recorded step unsafe, obsolete, or materially ambiguous.
5. Do not claim, reclaim, lock, register, rewrite, move, or delete anything merely to resume. If the continued work later needs another handoff, refresh the same workstream's snapshot and preserve every unrelated workstream.

## Origin

Adapted from [ToolMonsters/handoff-skill](https://github.com/ToolMonsters/handoff-skill), created by Yonathan Cohen (Tool Monsters) and distributed under the MIT License. This version retains the portable Markdown handoff and zero-invention principles, with repository-aware per-workstream snapshots and a lightweight resume workflow.
