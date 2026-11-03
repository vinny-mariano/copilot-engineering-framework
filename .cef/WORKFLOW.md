# CEF — Operational Workflow

## PURPOSE

Define the operational sequence for executing tasks under the Copilot Engineering Framework.

This workflow governs task progression from initial intake through planning, review, implementation, verification, red-team review and closure.

The canonical principles, severity model, confidence model, approval gates and authority rules are defined in `.cef/ENGINE.md`.

Detailed procedures are defined in the corresponding files under `.cef/prompts/`.

Metric definitions are governed by `.cef/docs/metrics/definitions.md`.

## REQUIRED CONTEXT

Before starting or resuming a task, read:

1. `.cef/ENGINE.md`
2. `.cef/WORKFLOW.md`
3. `.cef/TASK_STATE.md`

Read the relevant canonical procedure before executing each phase.

Read `.cef/docs/metrics/definitions.md` whenever recording or interpreting metric evidence.

If a required file cannot be located or read, report the problem and stop the affected operation.

Do not assume that referenced files have been loaded automatically.

---

# PHASE 0 — INTAKE

**Canonical procedure:** `.cef/prompts/intake.core.md`

### Objective

Understand the request, inspect the available context, identify uncertainties and prepare a structured task definition.

### Required actions

1. Execute the canonical Intake procedure.
2. Inspect the relevant repository context.
3. Identify the objective and expected outcome.
4. Establish acceptance criteria.
5. Identify scope, assumptions, dependencies and risks.
6. Establish the initial severity and confidence assessments.
7. Prepare the proposed task definition in memory.
8. Present the complete proposed definition to the human.
9. Request explicit authorization to record the approved task definition in `.cef/TASK_STATE.md`.
10. After authorization, record the information and verify the resulting file.

### TASK_STATE fields

During Intake, prepare and record the applicable fields:

- `Identification`: task ID, task name and creation date.
- `Objective`: expected outcome and acceptance criteria.
- `Scope`: initial scope and exclusions.
- `Information Provenance`: distinguish confirmed facts, repository evidence, AI suggestions, pending analysis, pending decisions and unknown information.
- `Assessment > Initial Assessment`: initial severity prediction, confidence prediction, assumptions and risks.
- `Implementation > Initial Direction`: preliminary implementation direction, clearly identified as a proposal.

Keep the following fields pending until their respective phases:

- `Plan`
- `Approved Strategy`
- `Human Approvals > Implementation`

Do not populate actual severity or current confidence with unverified assumptions.

### Restrictions

- Do not modify application source code.
- Do not install dependencies.
- Do not change application configuration.
- Do not request or grant implementation authorization.
- Do not treat authorization to record TASK_STATE as authorization to implement.

Implementation authorization belongs exclusively to Phase 2 — Review.

### Completion condition

The task definition has been explicitly authorized, recorded and verified.

Report:

`Intake recorded — implementation not authorized.`

---

# PHASE 1 — PLAN

### Objective

Develop a bounded implementation plan based on the approved task definition.

### Required actions

1. Read the current `.cef/TASK_STATE.md`.
2. Review the objective, acceptance criteria, scope, assumptions and risks.
3. Inspect the relevant application files and existing implementation patterns.
4. Identify affected components, contracts, dependencies and configuration.
5. Evaluate alternative implementation approaches when they materially affect risk or scope.
6. Select the smallest complete solution consistent with the approved objective.
7. Define the implementation sequence.
8. Define the verification strategy.
9. Identify potential approval gates under `.cef/ENGINE.md`.
10. Present the proposed plan to the human for review.

### Planning output

The proposed plan must identify:

- Objective.
- Files or components expected to change.
- Proposed implementation approach.
- Existing patterns to preserve.
- Expected contract or interface impact.
- Dependencies and configuration impact.
- Risks and assumptions.
- Severity and confidence assessment.
- Verification procedures.
- Acceptance criteria addressed by the plan.

### TASK_STATE handling

The proposed plan may be presented and discussed during this phase without modifying `.cef/TASK_STATE.md`.

Do not overwrite the initial severity or confidence predictions established during Intake.

If new evidence changes the assessment, explain the change and preserve both the initial assessment and the updated assessment separately.

The approved plan and strategy must be recorded in TASK_STATE during Phase 2, after explicit human authorization.

### Restrictions

- Do not modify application files.
- Do not install dependencies.
- Do not change application configuration.
- Do not interpret a proposed plan as implementation authorization.
- Do not expand scope without the applicable approval.

### Planning mode

Prefer Copilot Plan Mode when available.

If Plan Mode is unavailable, use a conversational planning process while preserving the same requirements.

---

# PHASE 2 — REVIEW

### Objective

Evaluate the proposed plan and obtain explicit human authorization before implementation.

### Required actions

Review:

1. Objective and expected outcome.
2. Acceptance criteria.
3. Approved scope and exclusions.
4. Repository evidence.
5. Existing implementation patterns.
6. Assumptions and unresolved questions.
7. Severity and confidence.
8. Proposed implementation strategy.
9. Expected file changes.
10. Risks and potential approval gates.
11. Verification strategy.

### Approval requirements

Present the complete plan and its relevant risks to the human.

Request an explicit decision on implementation authorization.

The approval request must make clear that authorization covers:

- Implementation of the reviewed plan within the approved scope.
- Recording the approved `Plan` and `Approved Strategy` in `.cef/TASK_STATE.md`.
- Recording the implementation approval and its evidence in the corresponding TASK_STATE fields.
- Updating task-state execution, validation and verification evidence as the authorized work progresses.

These permissions do not authorize:

- Scope expansion.
- Unapproved contract changes.
- Additional dependencies or configuration changes outside the approved plan.
- Operations requiring separate approval under `.cef/ENGINE.md`.
- Metrics collection or modification of historical records.
- TASK_STATE reset or deletion of historical records.

Any operation requiring an additional approval must follow the applicable ENGINE gate.

### TASK_STATE recording

After explicit approval:

1. Record the approved plan in `Plan`.
2. Record the approved implementation approach in `Approved Strategy`.
3. Record the approved scope in `Human Approvals > Implementation > Approved Scope`.
4. Record the decision and its evidence in `Human Approvals > Implementation`.
5. Verify that the information was recorded correctly.

If the approval is denied, do not implement.

If recording or verification fails, do not proceed to implementation.

### Completion condition

The implementation plan and its authorization have been recorded and verified.

Only now may Phase 3 begin.

---

# PHASE 3 — IMPLEMENT

### Objective

Implement the approved plan within the authorized scope while progressively preserving execution evidence.

### Standard prompt

Implement the approved plan for the task documented in `.cef/TASK_STATE.md`.

Use `.cef/TASK_STATE.md` as the authoritative task context.

Follow `.cef/ENGINE.md` and the applicable technology-specific instructions.

Modify only the application files required by the approved scope.

Do not expand scope or perform unrelated refactoring.

### Required behavior

1. Follow the approved implementation sequence.
2. Preserve existing architecture and conventions.
3. Prefer the smallest complete solution.
4. Make targeted changes.
5. Avoid unnecessary dependencies.
6. Respect all applicable approval gates.
7. Stop and request approval when a gate is triggered.
8. Report unexpected findings that materially affect the approved plan.
9. Do not silently change requirements or acceptance criteria.
10. Preserve relevant execution evidence as the work progresses.

### TASK_STATE handling

Update the task status to `implementing` when implementation begins.

Record the following progressively, using evidence available at the time:

#### Iteration Record

- Record each substantive work cycle.
- Identify the phase and work performed.
- Record the outcome and relevant evidence.
- Do not count every conversation message as a separate iteration.

#### Active Time Evidence

- Record active working time only when reliable evidence exists.
- Identify the activity, duration, evidence and measurement type.
- Distinguish measured values from estimates.
- Do not infer active working time from response latency or isolated timestamps.

#### Scope Changes

- Record proposed scope changes and their reasons.
- Record their impact and required authorization.
- Distinguish approved changes from unauthorized scope expansion.
- Do not treat an approved scope change as `scope_escape`.

#### Framework Rule Feedback

- Record rules that prevent, detect or correct relevant issues under `Rules Caught`.
- Record unnecessary effort, delay, ambiguity or obstruction under `Rules Friction`.
- Identify the rule and supporting evidence.
- Do not classify a rule as effective or ineffective without supporting evidence.

#### Execution Notes

Record material discoveries, implementation decisions, deviations and limitations.

Do not replace the approved plan with an unapproved alternative.

### Scope changes

If implementation reveals that the approved plan is insufficient:

1. Stop the affected operation.
2. Explain the technical reason.
3. Identify the proposed scope change and its impact.
4. Request explicit human approval when required by ENGINE.
5. Update the approved task context only after the applicable authorization.
6. Resume only within the newly authorized scope.

### Evidence integrity

- Preserve the original implementation authorization.
- Do not overwrite initial severity or confidence predictions.
- Record updated assessments separately when new evidence justifies them.
- Do not invent measurements or execution results.
- If evidence is unavailable, preserve the appropriate unknown or pending state.

---

# PHASE 4 — VERIFY

### Objective

Establish whether the implementation satisfies the approved acceptance criteria using actual evidence.

### Required actions

1. Set TASK_STATE `Status` to `verifying` when verification begins.
2. Read the approved acceptance criteria.
3. Review the verification procedures defined during planning.
4. Execute the relevant tests and validation procedures.
5. Record the commands and procedures actually executed.
6. Record each validation result separately.
7. Evaluate the overall result.
8. Identify verified and unverified acceptance criteria.
9. Identify remaining issues and limitations.
10. Report evidence and confidence accurately.

### TASK_STATE recording

Update the corresponding fields under `Validation Evidence`:

- `Planned`: expected tests and verification procedures.
- `Executed`: commands, tests and procedures actually performed.
- `Individual Results`: each validation, its result and supporting evidence.
- `Overall Results`: consolidated validation outcome and summary.

Update `Verification Summary`:

- `Verified Acceptance Criteria`.
- `Unverified Acceptance Criteria`.
- `Remaining Issues`.

Use the exact result values defined in `.cef/TASK_STATE.md`:

- `PASSED`
- `FAILED`
- `PARTIALLY PASSED`
- `NOT EXECUTED`

### First Implementation Evaluation

When an implementation is first evaluated against its applicable acceptance criteria:

1. Record the implementation being evaluated.
2. Identify the evaluation criteria.
3. Record the result and supporting evidence.
4. Update `Execution Evidence > First Implementation Evaluation`.

Use:

- `PASSED`
- `FAILED`
- `PARTIALLY PASSED`
- `NOT EVALUATED`
- `N/A`

Do not change this first evaluation retroactively when later corrections are made.

Subsequent corrections and evaluations belong in the validation evidence and execution notes.

### Assessment update

If verification provides evidence that changes the actual severity or current confidence:

- Record the updated value under `Assessment > Updated Assessment`.
- Preserve the original prediction.
- Record the evidence supporting the reassessment.
- Do not treat a change in confidence as proof that the initial prediction was incorrect.

### Restrictions

Do not claim a test passed unless it was actually executed and its result was established.

Do not treat the absence of reported errors as proof of successful validation.

Do not populate final metrics during this phase. Record execution evidence; metric consolidation belongs to Phase 6.

### Completion condition

Verification evidence has been recorded and the status of every applicable acceptance criterion has been evaluated.

Evaluation does not imply that every criterion passed.

If all applicable criteria are satisfied and no blocking issue remains, the task may be classified as completed.

If one or more applicable criteria remain unsatisfied, classify the task as incomplete rather than declaring it completed.

If a material human decision prevents reliable evaluation or classification, record the pending decision and do not proceed to closure.

Blocking issues must be explicitly assessed and documented. Their presence prevents completed-task classification when they leave applicable acceptance criteria unsatisfied.

---

# PHASE 5 — RED TEAM REVIEW

### Objective

Challenge the implementation and verification conclusions to identify defects, overlooked risks and unsupported assumptions.

### When required

Red Team Review is mandatory for HIGH and CRITICAL severity tasks.

For LOW and MEDIUM tasks, it may be used when the risk or uncertainty justifies additional scrutiny.

### Reviewer behavior

Act as an independent, skeptical reviewer.

Challenge:

- Whether the implementation satisfies the actual requirements.
- Whether the approved scope was respected.
- Whether existing contracts and patterns were preserved.
- Whether edge cases were overlooked.
- Whether validation evidence is sufficient.
- Whether the conclusions are supported by repository evidence.
- Whether regressions or unintended consequences are plausible.

### Restrictions

- Do not modify application files during the review.
- Do not silently change the approved implementation.
- Do not treat assumptions as verified facts.
- Do not dismiss findings without evidence.

### Findings

For each finding, report:

- Description.
- Severity.
- Supporting evidence.
- Potential impact.
- Recommended action.

Record the findings in `Verification Summary > Red Team Findings`.

When a framework rule catches a relevant issue, record it under `Execution Evidence > Framework Rule Feedback > Rules Caught`.

When a framework rule or review procedure creates unnecessary friction, record it under `Rules Friction`.

Avoid duplicate entries when the same finding or rule has already been recorded.

Resolve findings through the appropriate authorized workflow.

If a finding requires scope expansion or a gated operation, follow `.cef/ENGINE.md`.

### Completion condition

The review has been completed when required, and its findings have been recorded.

Blocking findings must be resolved before a task can be classified as completed.

Unresolved non-blocking findings must be explicitly disclosed.

An incomplete task may still proceed to administrative closure when its incomplete classification, unresolved issues and available evidence are accurately documented and no pending human decision prevents closure.

---

# PHASE 6 — CLOSE

**Canonical procedure:** `.cef/prompts/close-task.core.md`

### Objective

Close a task by consolidating applicable evidence, preserving historical records and metric integrity, and completing the required archival and administrative procedures.

### Preconditions

Before starting closure:

- Applicable verification has been completed or its limitations explicitly recorded.
- Acceptance criteria have been evaluated.
- Required Red Team Review has been completed.
- Blocking findings have been assessed and documented.
- Required human approvals exist.
- The task completion classification can be reliably established.
- No unresolved material human decision prevents the proposed closure operation.

A task does not need to be classified as COMPLETED for its administrative closure to proceed.

Incomplete tasks may be administratively closed when their classification and remaining issues are documented and all applicable closure requirements are satisfied.

A task classified as `PENDING HUMAN CLARIFICATION` must not proceed to READY, archival or reset until the relevant decision is resolved.

### Required actions

The following actions summarize the closure sequence. They do not replace, shorten or override the canonical Close Task procedure.

1. Execute the complete canonical Close Task procedure.
2. Read `.cef/docs/metrics/definitions.md`.
3. Inspect available repository and execution evidence.
4. Consolidate metric values from evidence recorded throughout the workflow.
5. Identify unknown, estimated, disputed and not-applicable values.
6. Distinguish completed tasks from incomplete framework evaluations.
7. Check for duplicate Task IDs.
8. Prepare the applicable metrics or framework evaluation record, or explicitly establish that it is not applicable.
9. Present the proposed record and supporting evidence to the human.
10. Obtain explicit approval before appending a persistent record.
11. Verify the resulting record.
12. Set Closure Status to `READY` only after applicable persistent records and required decisions have been resolved.
13. Prepare and verify the TASK_STATE archive.
14. Update the active TASK_STATE to `CLOSED` only after successful archive verification.
15. Obtain separate, explicit approval before resetting TASK_STATE.
16. Reset and verify the active task state only after all required checks succeed.

For incomplete tasks:

- Do not append a completed-task metrics row.
- Set the Metrics Record decision to `NOT APPLICABLE`, with the reason documented.
- Prepare a framework evaluation observation only when relevant and supported by evidence.
- Otherwise, set the observation decision to `NOT APPLICABLE`, with the reason documented.

For completed tasks:

- Prepare exactly one proposed completed-task metrics row.
- Use `Outcome = COMPLETED`.
- Do not invent alternative Outcome values.

### TASK_STATE handling

Update the applicable closure fields:

- `Closure > Task Completion Classification`.
- `Closure > Closure Status`.
- `Closure > Closure Decisions`.
- `Closure > Closure Transition Record`.

Do not mark a record as written and verified until its contents have been checked.

Do not mark an archive as created and verified until its existence and content have been checked against the original TASK_STATE snapshot.

The archived snapshot is immutable and represents the state at the time of archival. It may retain `Closure Status = READY`, `Archive = NOT PREPARED` and `TASK_STATE Reset = NOT REQUESTED`.

After archive verification, update the active TASK_STATE to `Closure Status = CLOSED`, `Archive = CREATED AND VERIFIED` and `TASK_STATE Reset = PENDING APPROVAL`.

Do not modify the archived snapshot to reflect subsequent transitions or reset decisions.

Do not mark TASK_STATE reset as completed before verifying the resulting blank template.

### Restrictions

- Do not invent metric values.
- Do not overwrite historical records.
- Do not reset TASK_STATE before verifying the archive.
- Do not delete historical records.
- Do not treat implementation approval as closure or reset approval.
- Do not claim closure succeeded if a required operation or verification failed.

### Version control

Version control operations are separate from task implementation and closure.

Do not create commits unless explicitly requested or authorized.

Durable architectural decisions should be documented through an appropriate Architecture Decision Record (ADR) when applicable.

---

# GENERAL RULES

## Human authority

Human approval is explicit and operation-specific.

Silence, implied consent or prior approval for a different operation do not constitute authorization.

Recording evidence already produced by an authorized operation does not grant permission to perform additional operations.

## Evidence

Distinguish clearly between:

- Human-confirmed information.
- Repository-verified facts.
- AI suggestions.
- Pending analysis.
- Pending human decisions.
- Unknown information.

Use the value states and definitions in `.cef/docs/metrics/definitions.md` when recording metric evidence.

## Conflicts

If canonical documents or instructions conflict:

1. Identify the conflicting sources.
2. Explain the impact.
3. Stop the affected operation.
4. Request clarification or an explicit decision.

Do not silently reconcile conflicting instructions.

## Reporting

Use the report format defined in `.cef/ENGINE.md`:

- Changed
- Validation
- Risks
- Confidence
