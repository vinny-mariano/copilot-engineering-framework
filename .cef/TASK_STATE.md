# TASK STATE

Ephemeral task context.

One ACTIVE block per task.

This file records the current task, its provenance, decisions, authorizations, execution evidence and verification results.

Update it progressively as the workflow advances. Do not wait until closure to reconstruct information that can be recorded when it becomes available.

Historical task records belong in the metrics archive, not in this file.

---

## ACTIVE

### Identification

Task ID:

Task Name:

Created:

Last Updated:

Status:  
planned | implementing | verifying | done

Status semantics:

- `planned`: task definition and planning are in progress or awaiting implementation authorization.
- `implementing`: authorized implementation is in progress.
- `verifying`: implementation is complete or ready for evaluation, and verification is in progress.
- `done`: all applicable task completion criteria have been satisfied.

Do not use `done` to indicate that administrative closure or TASK_STATE reset has been completed.

### Objective

Expected Outcome:

Acceptance Criteria:

### Scope

In Scope:

Out of Scope:

#### Scope Changes

Record each proposed or approved change to the original scope.

Change:

Reason:

Impact:

Authorization:  
NOT REQUESTED | PENDING | APPROVED | REJECTED | N/A

Approval Evidence / Reference:

Implementation Performed:

### Information Provenance

#### CONFIRMED

Information explicitly established by the human or supported by sufficient and unambiguous evidence.

Identify the source when confirmation is evidence-based.

#### VERIFIED IN REPOSITORY

Technical facts directly established through repository inspection or executed validation.

Record the relevant files, commands or validation evidence.

Repository verification does not establish human intent or approval.

#### AI SUGGESTION

Recommendations, interpretations or proposed solutions awaiting human approval.

#### PENDING ANALYSIS

Information requiring further investigation because sufficient evidence is not currently available.

#### PENDING HUMAN DECISION

Questions, conflicts or approvals requiring an explicit human response.

#### UNKNOWN

Information that cannot currently be established from available evidence.

Do not silently convert UNKNOWN into an assumption.

### Assessment

#### Initial Assessment

Severity Prediction:

Confidence Prediction:

Initial Assumptions:

Initial Risks:

#### Updated Assessment

Actual Severity:

Current Confidence:

Assessment Evidence:

Explain material changes from the initial assessment. Do not overwrite the original prediction.

### Implementation

Initial Direction:

Approved Strategy:

Plan:

Implementation Summary:

Files Changed:

### Human Approvals

#### TASK_STATE Recording

Decision:  
PENDING | APPROVED | REJECTED

Approved Content / Reference:

Evidence / Reference:

#### Implementation

Decision:  
NOT REQUESTED | PENDING | APPROVED | REJECTED

Approved Scope:

Evidence / Reference:

#### Additional Authorizations

Record any additional approval required by ENGINE.md, including scope expansion, contract changes or gated operations.

Operation:

Decision:  
PENDING | APPROVED | REJECTED

Approved Scope:

Evidence / Reference:

---

## EXECUTION EVIDENCE

Record evidence as it becomes available. Do not reconstruct measurements from unreliable recollection or isolated timestamps.

### Iteration Record

One entry represents a substantive work cycle, not an individual conversation message.

| Iteration | Phase | Work Performed | Result | Evidence |
|---|---|---|---|---|
| | | | | |

### Active Time Evidence

Record only reliable evidence of active working time.

| Activity / Phase | Duration (minutes) | Evidence | Measurement Type |
|---|---:|---|---|
| | | | MEASURED / ESTIMATED |

Total Active Time:

Measurement Limitations:

Do not infer active working time from response latency, elapsed conversation time or isolated timestamps.

### First Implementation Evaluation

Applicable only when an implementation was performed and evaluated.

First Implementation:

Evaluation Criteria:

Result:  
PASSED | FAILED | PARTIALLY PASSED | NOT EVALUATED | N/A

Evidence:

### Framework Rule Feedback

#### Rules Caught

Rules that prevented, detected or corrected a relevant issue.

| Rule | Issue or Risk | Evidence | Impact |
|---|---|---|---|
| | | | |

#### Rules Friction

Rules or procedures that caused unnecessary effort, delay, ambiguity or obstruction.

| Rule | Friction Observed | Evidence | Impact |
|---|---|---|---|

#### Unused Rules

Relevant rules that were not exercised during this task.

Record only when useful for framework evaluation. An unused rule is not automatically ineffective.

### Execution Notes

Record relevant events, deviations, decisions and evidence that do not fit the preceding fields.

---

## VALIDATION EVIDENCE

### Planned

Expected tests and verification procedures:

### Executed

Commands, tests and procedures actually performed:

### Individual Results

Record each validation separately.

Validation:

Result:  
PASSED | FAILED | PARTIALLY PASSED | NOT EXECUTED

Evidence:

### Overall Results

PASSED | FAILED | PARTIALLY PASSED | NOT EXECUTED

Summary:

### Verification Summary

Verified Acceptance Criteria:

Unverified Acceptance Criteria:

Remaining Issues:

Red Team Findings:

---

## CLOSURE

### Task Completion Classification

Classification:  
COMPLETED | INCOMPLETE | NOT APPLICABLE | PENDING HUMAN CLARIFICATION

Evidence:

Classification semantics:

- `COMPLETED`: all applicable task completion criteria have been satisfied.
- `INCOMPLETE`: one or more applicable completion criteria remain unsatisfied.
- `NOT APPLICABLE`: the task genuinely does not fall within the applicable task or workflow context.
- `PENDING HUMAN CLARIFICATION`: a material unresolved human decision prevents reliable classification.

Do not classify a task as COMPLETED merely because its administrative closure can proceed.

### Closure Status

Status:  
NOT READY | PENDING APPROVAL | READY | CLOSED

Closure Evidence:

Closure status semantics:

- `NOT READY`: applicable closure prerequisites or required records are incomplete.
- `PENDING APPROVAL`: a required human decision or authorization is outstanding.
- `READY`: applicable persistent records have been written and verified, and the task state is ready for archival.
- `CLOSED`: the archive has been created and verified, and the documentary closure has been completed.

`CLOSED` does not mean that TASK_STATE has been reset.

The task completion classification, task Status and Closure Status represent different dimensions and must not be treated as interchangeable.

### Closure Decisions

#### Metrics Record

NOT PREPARED | PENDING APPROVAL | APPROVED | WRITTEN AND VERIFIED | NOT APPLICABLE

#### Framework Evaluation Observation

NOT PREPARED | PENDING APPROVAL | APPROVED | WRITTEN AND VERIFIED | NOT APPLICABLE

#### Archive

NOT PREPARED | CREATED AND VERIFIED | FAILED | NOT APPLICABLE

#### TASK_STATE Reset

NOT REQUESTED | PENDING APPROVAL | APPROVED | COMPLETED

Closure decision semantics:

- `NOT PREPARED`: the operation has not been prepared or evaluated for applicability.
- `PENDING APPROVAL`: the proposed operation requires explicit human authorization.
- `APPROVED`: explicit human authorization has been obtained, but the operation has not yet been verified as complete.
- `WRITTEN AND VERIFIED`: the persistent metrics or observation record has been written and its contents checked.
- `CREATED AND VERIFIED`: the archive exists and its contents match the source snapshot.
- `COMPLETED`: TASK_STATE has been reset and the resulting blank template has been verified.
- `NOT APPLICABLE`: the operation genuinely does not apply to the task, and this determination is supported by evidence.

Do not mark an operation as completed without verification evidence.

A task may be administratively closed without a metrics row or framework observation when both are genuinely NOT APPLICABLE.

The archive must still preserve the available task history unless archiving itself is genuinely not applicable under an explicitly established procedure.

### Closure Transition Record

Record the relevant transitions and evidence when closure advances.

| Transition | Previous State | New State | Evidence / Reference |
|---|---|---|---|
| | | | |

The expected documentary closure sequence is:

1. Complete or classify the task.
2. Prepare and approve applicable persistent records.
3. Write and verify applicable persistent records.
4. Set Closure Status to `READY`.
5. Create and verify the archive snapshot.
6. Set Closure Status to `CLOSED` in the active TASK_STATE.
7. Obtain separate human approval for TASK_STATE reset.
8. Execute and verify the reset.

The archive is a snapshot of the state at the time of archival. It is not to be modified to reflect transitions or decisions made afterward.

If the active TASK_STATE is reset, the archived snapshot remains the historical evidence of the pre-reset state.

---

## METRICS

This section is a closure-stage consolidation of evidence recorded above and elsewhere.

Do not treat proposed values as approved values.

Follow `.cef/docs/metrics/definitions.md` and `.cef/prompts/close-task.core.md`.

### Core

time_min:

iterations:

acceptance_1st:

scope_escape:

### Calibration

sev_pred:

sev_actual:

conf_pred:

conf_actual:

### Framework Feedback

rules_caught:

rules_friction:

### Validation

validation_summary:

### Notes

observations:

### Metric Evidence and Confidence

For each proposed metric, identify its evidence source and whether the value is measured, estimated, UNKNOWN, PENDING HUMAN CLARIFICATION or N/A.

Do not replace the original execution evidence with the consolidated metric values.

---

## HISTORICAL RECORD

Historical task records must be preserved in the metrics archive.

Do not place multiple task histories in this active file.

Do not reset this file until the canonical closing procedure has verified the archive and obtained the required human approval.
