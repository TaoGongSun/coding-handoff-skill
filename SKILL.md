---
name: handoff
description: Create or resume a simple append-only coding handoff when the user asks for a handoff, 交接, resume, another session or model, or work must genuinely stop at a context, quota, or session boundary. Do not use merely because work is large, planned, multi-file, or involves Git, and do not use when the current run can finish the work.
---

# Handoff

Leave a portable Markdown note so another coding agent can continue without a state-management system.

## Create a handoff

1. Use the repository root as the project root. If there is no repository, use the current project root.
2. Create `.ai/handoffs/` if needed. Do not create `.ai/HANDOFF.md` or any other index, registry, database, lock, ownership record, or state file.
3. Choose a new filename in this form:

   `YYYY-MM-DD-HHMM-<short-topic>.md`

   Use local time and a short lowercase ASCII hyphenated topic. Check immediately before writing. If the name already exists, add `-2`, `-3`, and so on until the path is unused. Never overwrite or update an existing handoff.
4. Gather only facts supported by the current conversation or project. Inspect relevant files and Git state when useful. If something is uncertain, label it uncertain instead of guessing.
5. Write ordinary Markdown directly. Use whichever sections and order best preserve the work. Useful sections, when applicable, include:

   - Goal / Context
   - Current state
   - Important decisions
   - Completed
   - Verification
   - Remaining
   - Immediate next step
   - Constraints / pitfalls
   - Relevant files
   - Unstored drafts, patches, commands, or exact text needed to continue

   Omit empty sections. Preserve custom sections and their order. Do not parse, normalize, reorder, or reject the document because a suggested section is absent.
6. Prefer exact repository pointers over duplication. When work is reliably stored in the repository, record the precise path, modification status, and useful branch, commit, or diff context. Do not copy large source files or documents into the handoff. Include content verbatim only when it is not reliably stored elsewhere and the next agent truly needs the exact text.
7. Treat Git information as optional context, never as validity metadata. Later repository changes do not invalidate an old handoff.
8. The handoff operation may create only the new handoff file and its missing parent directory. Do not modify old handoffs, plans, source files, branches, commits, or Git configuration unless the user separately asks.
9. Report the new handoff path. Do not claim the work itself is complete unless verification supports that claim.

Never put secrets, tokens, credentials, or unnecessary private data in a handoff.

## Resume from a handoff

1. If the user names a handoff, read that exact file. Otherwise list `.ai/handoffs/`, choose the most relevant handoff, and use the newest timestamp when relevance is equal. Do not create an index.
2. Read the handoff, then inspect its referenced project files and current Git state only as needed.
3. Treat the current project as authoritative. If it differs from the handoff, state the difference and do not assume either side explains the other.
4. Continue from `Immediate next step`, or the clearest remaining action if that heading is absent. Stop for user input only when the current state makes the recorded step unsafe, obsolete, or materially ambiguous.
5. Do not claim, reclaim, lock, register, rewrite, move, or delete anything merely to resume. If the continued work later needs another handoff, create a new file and leave every earlier handoff unchanged.

## Origin

Adapted from [ToolMonsters/handoff-skill](https://github.com/ToolMonsters/handoff-skill), created by Yonathan Cohen (Tool Monsters) and distributed under the MIT License. This version retains the portable Markdown handoff and zero-invention principles, with repository-oriented, append-only storage and a lightweight resume workflow.
