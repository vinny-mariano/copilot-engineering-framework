# Copilot Engineering Framework (CEF) v1.1

A lightweight, evidence-driven engineering framework for GitHub Copilot.

CEF provides a structured approach to planning, implementing, verifying, measuring, and reviewing software engineering tasks with AI coding assistants.

Originally designed for:

- React
- Node.js
- Nginx

The framework is designed to:

- Reduce rework and unnecessary implementation iterations.
- Prevent scope creep.
- Reduce unnecessary context consumption.
- Improve first-pass implementation quality.
- Make AI-assisted development more predictable and auditable.
- Evaluate the effectiveness of engineering instructions through evidence.

---

## 1. Architecture

CEF separates decision-making, workflow execution, task context, metrics, and Copilot integration.

### Core framework

| Component | Responsibility |
|---|---|
| `.cef/ENGINE.md` | Core engineering principles, decision model, and behavioral constraints. |
| `.cef/WORKFLOW.md` | Operational workflow governing the task lifecycle. |
| `.cef/TASK_STATE.md` | Active task context, execution evidence, validation, and closure state. |
| `.cef/prompts/close-task.core.md` | Canonical procedure for task closure, metrics, observations, archival, and reset. |
| `.cef/docs/metrics/definitions.md` | Definitions, measurement rules, allowed values, and interpretation of metrics. |
| `.cef/docs/metrics/log.md` | Append-only historical task metrics and framework observations. |

### GitHub Copilot integration

| Component | Responsibility |
|---|---|
| `.github/copilot-instructions.md` | Global adapter connecting Copilot to the CEF. |
| `.github/instructions/` | Path-scoped instructions for specific technologies, directories, or file types. |
| `.github/prompts/` | Reusable prompts for recurring engineering operations. |

The integration layer provides Copilot with the relevant framework instructions. The `.cef` directory contains the governing engineering process and its persistent records.

### Architectural principle

The framework distinguishes three types of information:

- **Governing instructions:** define how the assistant should reason and operate.
- **Ephemeral task context:** records the current task and its execution state.
- **Persistent records:** preserve metrics, observations, and historical evidence.

These elements must not be treated as interchangeable.

---

## 2. Design Philosophy

CEF is based on three principles:

**Instructions guide behavior.**

The framework establishes constraints, decision criteria, and an expected execution process.

**Verification establishes facts.**

Implementation claims must be supported by inspection, tests, execution results, or other relevant evidence.

**Human review remains the final authority.**

The assistant may analyze, recommend, and prepare changes, but decisions requiring human authorization must remain pending until explicitly approved.

CEF does not assume that following instructions guarantees correct implementation. Its effectiveness must be evaluated through actual results.

---

## 3. Framework Goals

The objective is not simply to minimize token consumption.

The objective is to improve engineering outcomes:

- Fewer unnecessary iterations.
- Less rework.
- Better scope control.
- Higher first-pass acceptance.
- More reliable verification.
- Better alignment between predicted and actual technical impact.
- Sustainable and useful engineering instructions.

Metrics and observations exist to evaluate whether the framework achieves these objectives.

---

## 4. Framework Lifecycle

The CEF lifecycle consists of six operational phases.

| Phase | Purpose |
|---|---|
| 0. Initialization | Load governing instructions and establish task context. |
| 1. Assessment | Understand the request, scope, severity, and confidence. |
| 2. Planning | Define the implementation approach and acceptance criteria. |
| 3. Implementation | Execute the authorized changes within scope. |
| 4. Verification | Evaluate implementation against acceptance criteria. |
| 5. Review | Assess findings, disclose unresolved issues, and classify the outcome. |
| 6. Closure | Record applicable metrics, observations, archive the task, and handle reset authorization. |

The detailed and authoritative procedures are defined in `.cef/WORKFLOW.md`.

The following guide explains how to use these phases in practice.

---

## 5. How to Use CEF

### Step 1 — Start a new task

Before requesting implementation, ensure that Copilot has access to the framework instructions.

Start by providing a clear task request, including:

- What needs to be changed.
- Why the change is necessary.
- Relevant technical context.
- Known constraints.
- Expected behavior.

Ask Copilot to follow the CEF workflow.

Example:

> Follow the Copilot Engineering Framework. Analyze this request, assess its severity and confidence, identify the affected scope, and prepare the task plan before implementation.

The assistant should consult the governing documents and initialize the active task context in `.cef/TASK_STATE.md`.

Do not begin implementation before the required assessment and planning steps have been completed and authorization has been obtained.

### Step 2 — Assess the task

Copilot should analyze the request and establish:

- Task objective.
- Expected outcome.
- Scope and affected components.
- Constraints and dependencies.
- Potential risks.
- Initial severity prediction.
- Initial confidence assessment.

Severity and confidence are separate dimensions.

Severity estimates the potential impact of the task or issue.

Confidence represents the strength of the evidence supporting the technical assessment.

The initial predictions must be preserved. They must not be silently replaced by later assessments.

### Step 3 — Plan the implementation

Before changing files, Copilot should:

1. Inspect the relevant code and instructions.
2. Identify dependencies and integration points.
3. Define the implementation approach.
4. Identify potential regressions.
5. Establish measurable acceptance criteria.
6. Identify the validation strategy.

The plan must remain within the authorized scope.

If implementation requires a material scope change or an unresolved human decision, Copilot must request clarification rather than silently expanding the task.

### Step 4 — Authorize and implement

Once the plan is accepted, authorize implementation.

Copilot should:

- Follow the approved plan.
- Respect global and path-scoped instructions.
- Modify only the necessary files.
- Avoid unrelated refactoring.
- Preserve existing behavior unless a change is explicitly required.
- Report relevant deviations and blockers.

The active task status should reflect the current execution phase:

- `planned`
- `implementing`
- `verifying`
- `done`

`done` means that all applicable task completion criteria have been satisfied. It does not mean that administrative closure or reset has been completed.

### Step 5 — Verify the implementation

Verification is a mandatory phase, not an optional final check.

Copilot should evaluate each applicable acceptance criterion using appropriate evidence, such as:

- Automated tests.
- Build results.
- Static analysis.
- Type checking.
- Runtime behavior.
- Code inspection.
- Relevant integration checks.

For each criterion, record whether it was satisfied and identify the supporting evidence.

Do not treat an attempted test as a successful test.

Do not claim that functionality works merely because code was generated or modified.

If a criterion remains unsatisfied, the task must not be classified as completed.

### Step 6 — Review and classify the outcome

After verification, assess the findings and classify the task.

The task completion classification has four possible values:

| Classification | Meaning |
|---|---|
| `COMPLETED` | All applicable completion criteria were satisfied. |
| `INCOMPLETE` | One or more applicable completion criteria remain unsatisfied. |
| `NOT APPLICABLE` | The task genuinely does not fall within the applicable task or workflow context. |
| `PENDING HUMAN CLARIFICATION` | A material unresolved human decision prevents reliable classification. |

An incomplete task may still be administratively closed if its status and remaining issues are properly documented and no material human decision remains pending.

Administrative closure must never be used to represent an incomplete task as completed.

---

## 6. Task Closure: An Independent Process

Task completion and administrative closure are separate dimensions.

A task can be completed without having been archived.

A task can also be administratively closed while remaining incomplete, provided the applicable closure requirements are satisfied.

CEF uses the following closure states:

| Closure Status | Meaning |
|---|---|
| `NOT READY` | Required closure prerequisites or records are incomplete. |
| `PENDING APPROVAL` | A required human authorization is outstanding. |
| `READY` | Applicable persistent records have been written and verified; the task is ready for archival. |
| `CLOSED` | The archive has been created and verified, completing documentary closure. |

### Canonical closure procedure

Use `.cef/prompts/close-task.core.md` to execute the complete closure procedure.

This prompt is the authoritative operational procedure. Summaries or abbreviated instructions must not replace, shorten, or override it.

The closure procedure includes:

1. Inspect the task state and relevant execution evidence.
2. Confirm the task completion classification.
3. Determine whether standardized metrics apply.
4. Determine whether a framework evaluation observation applies.
5. Present proposed persistent records for human approval when required.
6. Write approved records to the appropriate files.
7. Verify the written records.
8. Establish `Closure Status: READY` when all applicable prerequisites are satisfied.
9. Create an archival snapshot.
10. Verify that the archive matches the source snapshot.
11. Update the active task state to `CLOSED`.
12. Request separate human authorization before resetting `TASK_STATE.md`.
13. Reset the active task state only after explicit authorization.
14. Verify the resulting blank template.

### Metrics and incomplete tasks

A completed task receives exactly one standardized metrics record with:

`Outcome = COMPLETED`

An incomplete task must not receive a completed-task metrics record.

Instead:

- `Metrics Record` must be `NOT APPLICABLE`, with the reason documented.
- A framework evaluation observation should be recorded when relevant.
- If no observation applies, document why it is `NOT APPLICABLE`.

`NOT APPLICABLE` must never be used to conceal missing evidence, unresolved decisions, or unavailable information.

### Archiving and reset are separate

The archive preserves the task history and its closure state.

The archive must be created and verified before documentary closure is considered complete.

The active `TASK_STATE.md` must then reflect the closed state.

Resetting `TASK_STATE.md` is a separate operation requiring explicit human authorization.

A successful archive does not automatically authorize a reset.

**Important:** `CLOSED` does not mean that the active task state has been reset.

---

## 7. Metrics and Framework Evaluation

CEF collects metrics to evaluate engineering outcomes and the effectiveness of its instructions.

The complete definitions and measurement rules are maintained in:

`.cef/docs/metrics/definitions.md`

The persistent historical records are maintained in:

`.cef/docs/metrics/log.md`

### Core metrics

| Metric | Purpose |
|---|---|
| `acceptance_1st` | Measures whether the first implementation was accepted without substantive correction. |
| `iterations` | Counts substantive task execution cycles. |
| `scope_escape` | Identifies implementation outside the authorized scope. |
| `sev_pred` | Records the initial severity prediction. |
| `sev_actual` | Records severity established after sufficient investigation. |
| `conf_pred` | Records initial assessment confidence. |
| `conf_actual` | Records confidence after evidence evaluation. |
| `time_min` | Records active task execution time when reliably available. |
| `rules_caught` | Identifies instructions or rules that prevented an issue or undesirable behavior. |
| `friction` | Records unnecessary constraints, confusion, or workflow obstacles. |

### Metric value integrity

Metrics must be based on available evidence.

The following values have distinct meanings:

- `0`: reliable evidence establishes that no substantive execution cycle occurred.
- `UNKNOWN`: a value should exist but cannot be reliably established.
- `PENDING HUMAN CLARIFICATION`: a human decision is required.
- `N/A`: the metric genuinely does not apply, with justification.

These values are not interchangeable.

Missing information must not be converted into zero or `N/A` merely to complete a record.

### Append-only historical log

The metrics log is append-only.

Existing task records must not be silently rewritten, deleted, or recalculated.

Corrections must follow the documented change-control rules while preserving historical integrity.

Every completed task must have exactly one corresponding standardized metrics record.

Incomplete tasks must not be represented as completed records.

---

## 8. Framework Review and Calibration

CEF is intended to evolve through evidence rather than subjective impressions.

Periodic reviews should examine:

- First-pass acceptance.
- Number of substantive iterations.
- Scope escape frequency.
- Severity prediction accuracy.
- Confidence calibration.
- Rules that consistently prevent problems.
- Rules that generate unnecessary friction.
- Workflow sustainability.
- Repeated implementation or verification failures.

The review should distinguish between:

1. A rule that is ineffective.
2. A rule that is incorrectly applied.
3. A lack of evidence.
4. A problem caused by the underlying project or environment.
5. A limitation of the AI assistant.

Do not modify framework rules simply because one task produced an unfavorable result.

Changes should be supported by repeated evidence and documented reasoning.

---

## 9. Practical Usage Reference

The following prompts can be used as starting points when interacting with Copilot.

### Start a task

> Follow CEF v1.1. Initialize the task context, analyze the request, assess severity and confidence, identify the scope, and prepare an implementation plan. Do not implement before authorization.

### Review the plan

> Review the proposed plan against the task objective, authorized scope, constraints, dependencies, and acceptance criteria. Identify gaps before implementation.

### Authorize implementation

> The plan is approved. Proceed with implementation within the authorized scope and follow the CEF instructions.

### Verify the implementation

> Start the verification phase. Evaluate every applicable acceptance criterion and provide evidence for each result. Identify failed, untested, and unresolved criteria. Do not claim success without evidence.

### Review the outcome

> Review the execution and verification evidence. Classify the task as COMPLETED or INCOMPLETE, identify unresolved issues, and prepare the required documentation.

### Close the task

> Execute the canonical Close Task procedure defined in `.cef/prompts/close-task.core.md`. Follow all approval, metrics, observation, archival, and reset requirements. Do not skip steps or assume human authorization.

These prompts are examples of interaction patterns. They do not replace the governing instructions or canonical procedures.

---

## 10. Operational Rules

The following principles apply throughout the framework:

- Do not implement without an authorized plan.
- Do not expand scope without authorization.
- Do not invent evidence, test results, metrics, or historical information.
- Do not confuse implementation attempts with successful verification.
- Do not classify incomplete work as completed.
- Do not use `N/A` to conceal missing information.
- Do not rewrite historical metrics silently.
- Do not treat administrative closure as task completion.
- Do not treat archival as permission to reset task state.
- Do not reset `TASK_STATE.md` without explicit human authorization.
- Do not claim operational validation of CEF without empirical testing.

When instructions conflict, follow the governing hierarchy defined in `.cef/ENGINE.md` and the canonical procedures referenced by the framework.

---

## 11. Versioning and Change Control

CEF changes must preserve traceability and historical integrity.

Changes to governing instructions, workflow rules, metric definitions, or closure procedures should be evaluated as framework changes rather than ordinary task modifications.

Before changing the framework:

1. Identify the problem.
2. Collect supporting evidence.
3. Determine which components are affected.
4. Assess potential regressions and inconsistencies.
5. Propose the smallest coherent change.
6. Review cross-document consistency.
7. Preserve historical records.
8. Verify the resulting documentation.

Documentation corrections, broken references, and structural defects should be distinguished from changes to the framework's governing behavior.

A version should not be considered operationally validated merely because its documentation is internally consistent.

---

## 12. Current Framework Status

CEF v1.1 establishes the current documented architecture, workflow, metrics model, and closure procedure.

The documentation has undergone a cross-document consistency review, including verification of the historical task records T-001 through T-005.

This establishes a documented baseline, not proof of operational effectiveness.

The next validation stage is empirical testing with GitHub Copilot.

Those tests should evaluate whether the assistant:

- Correctly loads and follows the framework instructions.
- Maintains task state across workflow phases.
- Respects authorization and scope boundaries.
- Performs evidence-based verification.
- Applies the completion and closure classifications correctly.
- Executes the canonical closure procedure.
- Preserves metrics and historical records.
- Requests human authorization when required.

Only observed test results should be used to establish operational effectiveness.

---

## 13. Final Principle

CEF is not intended to replace engineering judgment.

It provides a repeatable structure for applying engineering discipline to AI-assisted software development.

**Plan deliberately. Implement within scope. Verify with evidence. Measure outcomes. Preserve history. Keep human authorization explicit.**
