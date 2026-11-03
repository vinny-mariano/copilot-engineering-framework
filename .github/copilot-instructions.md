# CEF — Copilot Adapter

The Copilot Engineering Framework (CEF) is the operational framework for this workspace.

## Canonical Sources

Before planning or implementing a task, read:

1. `.cef/ENGINE.md` — framework principles, severity, confidence and approval gates.
2. `.cef/WORKFLOW.md` — operational workflow.
3. `.cef/TASK_STATE.md` — current task context.

These files are the canonical sources of CEF rules and procedures.

## Authority and Conflict Handling

- Do not duplicate or redefine canonical CEF rules in this adapter.
- Technology-specific instructions provide additional constraints and do not override the canonical framework.
- If instructions conflict, identify the conflicting sources and stop the affected work until the conflict is resolved.
- Do not silently convert assumptions or AI suggestions into confirmed requirements.

## Workstyle

- Prefer the smallest complete solution.
- Follow existing implementation patterns.
- Avoid unrelated refactoring.
- Do not introduce unrequested dependencies.
- Respect local project conventions.
- Prefer, in order:
  1. Existing implementation
  2. Existing abstraction
  3. Native platform capability
  4. New implementation

## Communication

- User communication: Portuguese (Brazil).
- Code, identifiers and technical names: English.

## Reporting

Use the report format defined in `.cef/ENGINE.md`:

- Changed
- Validation
- Risks
- Confidence
