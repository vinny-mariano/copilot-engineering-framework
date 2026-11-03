---
name: CEF Intake
description: Start the canonical CEF task intake, investigation and approval procedure.
---

# CEF Intake — Adapter

Execute the canonical Intake procedure defined in:

`.cef/prompts/intake.core.md`

## Required Context

Before starting, read the complete contents of:

1. `.cef/ENGINE.md`
2. `.cef/WORKFLOW.md`
3. `.cef/TASK_STATE.md`
4. `.cef/prompts/intake.core.md`

Do not begin the procedure if a required file cannot be located or read. Report the problem and stop the affected operation.

## Execution Rules

- Follow the canonical Intake procedure in its entirety.
- Treat `.cef/prompts/intake.core.md` as the single source of truth for Intake operations.
- Do not omit, duplicate or redefine canonical procedures.
- Preserve information provenance and distinguish human-confirmed decisions from repository evidence and AI suggestions.
- Do not invent missing requirements, repository facts or human approvals.
- Prepare the proposed TASK_STATE in memory before requesting authorization to record it.
- Obtain explicit human authorization before writing to `.cef/TASK_STATE.md`.
- During Intake, request authorization only for recording the approved task definition.
- Do not request or grant implementation authorization during Intake.
- Implementation authorization belongs exclusively to Phase 2 — Review, as defined in `.cef/WORKFLOW.md`.
- Do not modify application source code, install dependencies or change application configuration during Intake.
- Respect all applicable approval gates defined in `.cef/ENGINE.md`.
- If instructions conflict, identify the conflicting sources and stop the affected operation.

## Authority

This adapter does not grant implementation permission.

The canonical Intake procedure and applicable human approvals determine which operations are authorized.

Do not replace canonical content with assumed instructions, abbreviated procedures or memorized versions.
