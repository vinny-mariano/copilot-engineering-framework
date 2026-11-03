---
name: CEF Close Task
description: Close a verified CEF task, consolidate evidence, preserve metrics and archive task state.
---

# CEF Close Task — Adapter

Execute the canonical closing procedure defined in:

`.cef/prompts/close-task.core.md`

## Required Context

Before starting, read the complete contents of:

1. `.cef/ENGINE.md`
2. `.cef/WORKFLOW.md`
3. `.cef/TASK_STATE.md`
4. `.cef/docs/metrics/definitions.md`
5. `.cef/docs/metrics/log.md`
6. `.cef/docs/metrics/review.md`
7. Inspect `.cef/docs/metrics/archive/`.
8. Read the complete `.cef/prompts/close-task.core.md`.

Inspect relevant task observation records when they exist.

Do not begin the procedure if a required file cannot be located or read. Report the problem and stop the affected operation.

## Execution Rules

- Follow the canonical closing procedure exactly.
- Treat `.cef/prompts/close-task.core.md` as the single source of truth for closure operations.
- Treat `.cef/docs/metrics/definitions.md` as the single source of truth for metric definitions.
- Consolidate available evidence before asking the human for information.
- Do not ask the human to repeat information already established in reliable records.
- Distinguish completed tasks from incomplete framework evaluations.
- Do not invent measurements or silently resolve conflicting evidence.
- Preserve UNKNOWN, estimated and N/A distinctions.
- Do not overwrite existing metrics records.
- Obtain explicit human approval before appending metrics or persistent framework evaluation records.
- Do not reset TASK_STATE without a verified archive and explicit human approval.
- If a required file cannot be located or read, report the problem and stop the affected operation.
- If instructions conflict, identify the conflicting sources and stop the affected operation until the conflict is resolved.

The canonical core and metric definitions are the authoritative sources for this procedure.
