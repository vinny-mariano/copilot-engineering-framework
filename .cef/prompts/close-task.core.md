# Close Task — Canonical Procedure

## 1. Purpose

This prompt defines the canonical procedure for closing a CEF task.

The procedure separates three independent dimensions:

1. **Task completion:** whether the task's acceptance criteria were satisfied.
2. **Administrative closure:** whether the task's evidence, records, and archival requirements have been processed.
3. **Framework evaluation:** whether the task produced evidence relevant to evaluating or improving CEF.

Administrative closure does not imply successful task completion.

A task may be administratively closed while remaining incomplete, provided that its outcome is explicitly classified, documented, and no unresolved human decision blocks closure.

This procedure is authoritative for task closure. Short summaries or workflow references do not replace, shorten, or override it.

## 2. Required Sources

Before beginning closure, inspect the relevant current versions of:

1. `.cef/ENGINE.md`
2. `.cef/WORKFLOW.md`
3. `.cef/TASK_STATE.md`
4. `.cef/docs/metrics/definitions.md`
5. `.cef/docs/metrics/log.md`
6. The task's relevant implementation, review, and validation evidence.
7. Relevant framework evaluation observations.
8. Existing archive records, when applicable.

Use the actual project files and available task evidence.

Do not assume that an instruction, file, or reference was loaded or followed merely because it exists in the repository.

## 3. Evidence Hierarchy

Use evidence in the following order of reliability:

1. Directly observable implementation and validation results.
2. Explicit acceptance criteria and task requirements.
3. Recorded task state and chronological task history.
4. Review findings and documented decisions.
5. Explicit user or human clarification.
6. Reasonable conclusions supported by the preceding evidence.

Do not invent missing evidence.

Do not treat an assumption as a verified fact.

When sources conflict, identify the conflict and determine whether human clarification is required.

A material unresolved conflict must not be silently resolved by choosing the most convenient interpretation.

## 4. Task Completion Classification

Evaluate every applicable acceptance criterion individually.

Classify task completion using exactly one of the following:

- `COMPLETED`
- `INCOMPLETE`
- `NOT APPLICABLE`
- `PENDING HUMAN CLARIFICATION`

### 4.1 COMPLETED

Use `COMPLETED` only when all applicable acceptance criteria are satisfied and supported by evidence.

A task must not be classified as completed merely because:

- The implementation appears plausible.
- The main code change was made.
- The task was administratively closed.
- Validation was skipped.
- A blocking issue remains unresolved.

### 4.2 INCOMPLETE

Use `INCOMPLETE` when one or more applicable acceptance criteria have not been satisfied.

Document:

- Which criteria remain unmet.
- What work remains.
- Which validations were performed.
- Which validations were not performed.
- Known blockers and unresolved risks.

An incomplete task may proceed to administrative closure when it is properly documented and no human decision is pending.

An incomplete task must never be represented as a completed task in the standardized metrics log.

### 4.3 NOT APPLICABLE

Use `NOT APPLICABLE` only when the task or criterion genuinely does not apply.

Document the reason.

Do not use `NOT APPLICABLE` to conceal missing evidence, unfinished work, an unknown result, or an unresolved decision.

### 4.4 PENDING HUMAN CLARIFICATION

Use `PENDING HUMAN CLARIFICATION` when a material decision, interpretation, approval, or clarification from a human is necessary before the task can be reliably classified or closed.

Do not proceed through blocked closure, archival, or reset steps while a required human decision remains pending.

## 5. Metric Preparation

Consult `.cef/docs/metrics/definitions.md` for canonical metric definitions and allowed representations.

Consult `.cef/docs/metrics/log.md` for the standardized record schema and historical context.

Every metric must be supported by evidence.

Do not invent, estimate without support, or infer a value merely to fill a field.

### 5.1 Acceptance 1st

Determine whether applicable acceptance criteria were satisfied on the first substantive implementation attempt.

Use the representations permitted by `definitions.md`.

- `Y`: supported evidence establishes first-attempt acceptance.
- `N`: supported evidence establishes that the first substantive attempt did not satisfy the applicable criteria.
- `UNKNOWN`: the value should exist but cannot be established from available evidence.
- `PENDING HUMAN CLARIFICATION`: a required human decision or clarification is outstanding.
- `N/A`: only when genuinely inapplicable, with the reason documented and required clarification or approval obtained.

Do not assume that the first recorded implementation was successful merely because no earlier attempt is documented.

### 5.2 Scope Escape

Determine whether the implementation exceeded the agreed task scope.

Use the representations permitted by `definitions.md`.

- `Y`: evidence establishes that implementation exceeded the agreed scope without an applicable approved scope adjustment.
- `N`: evidence establishes that implementation remained within the agreed scope.
- `UNKNOWN`: the value should exist but cannot be established.
- `PENDING HUMAN CLARIFICATION`: the scope or approval status requires human clarification.
- `N/A`: only when genuinely inapplicable, with the reason documented and required clarification or approval obtained.

Do not classify an explicitly approved scope adjustment as scope escape without evaluating the agreed scope.

### 5.3 Severity Mapping

Keep initial predicted severity and final actual severity separate.

Map the evidence independently to:

- `sev_pred`: initial predicted severity.
- `sev_actual`: final assessed severity.

Use only the severity categories defined in `definitions.md`.

For each field:

- Record the applicable category when supported by evidence.
- Use `UNKNOWN` when the value should exist but cannot be established.
- Use `PENDING HUMAN CLARIFICATION` when a human decision or clarification is required.
- Use `N/A` only when the metric is genuinely inapplicable, the reason is documented, and the required human clarification or approval has been obtained.

Do not use `N/A` merely because:

- The task is incomplete.
- The impact is unknown.
- Evidence is missing.
- The final assessment has not been performed.

Do not copy the initial prediction into the actual severity field without evidence supporting that final assessment.

### 5.4 Confidence Mapping

Keep initial predicted confidence and final actual confidence separate.

Map the evidence independently to:

- `conf_pred`: initial confidence assessment.
- `conf_actual`: final confidence assessment.

Use only the confidence categories defined in `definitions.md`.

For each field:

- Record the applicable category when supported by evidence.
- Use `UNKNOWN` when the value should exist but cannot be established.
- Use `PENDING HUMAN CLARIFICATION` when a human decision or clarification is required.
- Use `N/A` only when the metric is genuinely inapplicable, the reason is documented, and the required human clarification or approval has been obtained.

Do not use `N/A` merely because the task is incomplete, evidence is missing, or confidence cannot be established.

Do not treat predicted confidence as final confidence.

### 5.5 Iterations Mapping

Record the number of substantive implementation cycles.

A substantive implementation cycle is a meaningful attempt to implement or modify the solution, not every message, question, review comment, or clarification.

Use the following representations:

- A non-negative integer when the count is supported by reliable evidence.
- `0` when reliable evidence establishes that no substantive implementation cycle occurred.
- `UNKNOWN` when a count should exist but cannot be established from available evidence.
- `PENDING HUMAN CLARIFICATION` when conflicting evidence or a required human decision prevents a reliable classification.
- `N/A` only when the metric is genuinely inapplicable and the reason is documented.

These values are distinct:

- `0` is a known numeric result.
- `UNKNOWN` means the value cannot be established.
- `PENDING HUMAN CLARIFICATION` means a decision or clarification is required.
- `N/A` means the metric genuinely does not apply.

Do not count every conversation message as an iteration.

Do not invent or estimate an iteration count.

### 5.6 Active Time Mapping

Record active task time in minutes when supported by available evidence.

Use the following representations:

- A non-negative numeric value when reasonably established.
- `UNKNOWN` when active time should have been recorded but cannot be established.
- `PENDING HUMAN CLARIFICATION` when clarification is required.
- `N/A` only when active time is genuinely inapplicable and the reason is documented.

Do not use `N/A` merely because time was not recorded.

Do not equate elapsed calendar time with active work time without supporting evidence.

Any approximate value must be supported by the task history and must be clearly identifiable as approximate where the schema permits.

### 5.7 Rules Caught and Rules Friction

Identify framework rules that demonstrably caught, prevented, or corrected an issue.

Record only rules supported by observable evidence.

Identify framework rules that introduced unnecessary friction.

Do not classify a justified safeguard, required review, or necessary validation step as friction solely because it required additional work.

Use the representation permitted by `definitions.md` when no applicable rule was identified.

### 5.8 Validation Summary

Summarize validation based on actual evidence.

Distinguish clearly between:

- Validation passed.
- Validation failed.
- Validation partially passed.
- Validation not performed.
- Validation blocked.
- Validation pending.

Do not claim that validation passed when it was not performed.

Do not treat administrative closure as technical validation.

### 5.9 Missing Information

Apply the following distinction consistently across all metrics:

- `UNKNOWN`: the value should exist, but available evidence does not establish it.
- `PENDING HUMAN CLARIFICATION`: a human decision or clarification is necessary.
- `N/A`: the metric is genuinely inapplicable, with a documented reason and required human clarification or approval.
- `0`: a known numeric value, used only when reliable evidence establishes zero.

Never substitute one of these representations for another.

Do not use `N/A` as a general-purpose missing-data value.

## 6. Framework Evaluation Observation

Determine whether the task produced relevant evidence about CEF itself.

Examples include:

- Ambiguous or missing instructions.
- Rules that caught or failed to catch an issue.
- Repeated clarification requirements.
- Unnecessary process friction.
- Workflow inconsistencies.
- Validation weaknesses.
- Unexpected Copilot behavior.
- Opportunities to improve reliability or reduce manual work.

An observation must be based on evidence.

Do not create an observation merely to produce a record.

For an incomplete task, an observation may still be applicable.

If an observation is relevant, prepare a record consistent with the schema in `.cef/docs/metrics/log.md`.

If no observation is applicable, set `Framework Evaluation Observation` to `NOT APPLICABLE` and document the reason.

## 7. Task ID and Duplicate Checks

Before writing any persistent record:

1. Confirm the Task ID.
2. Search the metrics log for the Task ID.
3. Search relevant framework evaluation records for an existing observation.
4. Check whether an equivalent record has already been written.
5. Resolve any duplicate or identity conflict before proceeding.

A duplicate Task ID in the standardized metrics log blocks the creation of another standardized row for that task.

Do not silently overwrite an existing record.

If the identity or uniqueness of a record cannot be established, request human clarification.

## 8. Human Approval Before Persistent Writes

Present the proposed closure classification, metric values, framework evaluation observation, and relevant evidence for human review.

Obtain explicit human approval before writing applicable persistent metrics or framework evaluation records.

Approval must be clear and specific.

Do not interpret silence, an ambiguous response, or a request for further analysis as approval.

If approval is pending:

- Set the applicable record status to `PENDING APPROVAL`.
- Keep closure from advancing to `READY`.
- Do not create the archive snapshot.
- Do not reset `TASK_STATE.md`.

If clarification is required, use `PENDING HUMAN CLARIFICATION` and stop the blocked procedure until it is resolved.

## 9. Persistent Record Preparation

After the required human approval:

### 9.1 Completed Task

For a task classified as `COMPLETED`:

1. Prepare exactly one standardized metrics row.
2. Set `Outcome` to `COMPLETED`.
3. Append the row to `.cef/docs/metrics/log.md`.
4. Verify the persisted row.
5. Confirm that the Task ID appears exactly once in the standardized metrics records.

Do not create a standardized completed-task row for an incomplete task.

### 9.2 Incomplete Task

For a task classified as `INCOMPLETE`:

1. Do not append a standardized completed-task metrics row.
2. Set `Metrics Record` to `NOT APPLICABLE`.
3. Document why the task is incomplete.
4. Determine whether a framework evaluation observation is relevant.
5. If relevant, prepare, approve, append, and verify that observation.
6. If no observation is relevant, set `Framework Evaluation Observation` to `NOT APPLICABLE` and document the reason.

An incomplete task may proceed to administrative closure only when its state and remaining work are clearly documented and no human decision is pending.

### 9.3 Not Applicable Records

Use `NOT APPLICABLE` only when the corresponding record or measurement genuinely does not apply.

Document the reason.

Do not use it to avoid recording an unknown value, bypass a required approval, or conceal incomplete work.

### 9.4 Verification

After each persistent write:

- Re-read the affected record.
- Compare it with the approved content.
- Confirm the Task ID and field values.
- Confirm that no existing historical record was changed.
- Confirm that the record is in the intended location.

Do not mark a record as written and verified until this check is complete.

## 10. Closure Readiness

Evaluate the closure conditions in `TASK_STATE.md`.

The task may reach `Closure Status = READY` only when:

- Task completion classification has been established.
- Applicable acceptance criteria have been evaluated.
- Remaining incomplete work is documented, if applicable.
- No required human clarification is pending.
- Required human approval has been obtained.
- Applicable metrics records have been written and verified, or explicitly marked `NOT APPLICABLE` with a documented reason.
- Applicable framework evaluation observations have been written and verified, or explicitly marked `NOT APPLICABLE` with a documented reason.
- The Task ID and record integrity checks have passed.
- All other applicable closure requirements are satisfied.

`READY` means that the persistent records are prepared and verified and the task is ready for archival.

`READY` does not mean that the archive has already been created.

If any condition is unmet, do not set closure to `READY`.

## 11. Archive Snapshot

Create the archive snapshot only after closure reaches `READY`.

The snapshot must preserve the pre-archive state.

At the time of snapshot creation, the expected state is:

- `Closure Status = READY`
- `Archive = NOT PREPARED`
- `TASK_STATE Reset = NOT REQUESTED`

The snapshot must capture the relevant task state and evidence without modifying the historical content.

After creating the archive:

1. Verify that the archive exists.
2. Verify that its contents match the intended snapshot.
3. Verify that the snapshot preserves the expected pre-archive state.
4. Confirm that no unrelated archive or historical record was overwritten.

If archive creation or verification fails:

- Set `Archive = FAILED`.
- Do not claim that the task is closed.
- Do not reset `TASK_STATE.md`.
- Report the failure and required next action.

The archived snapshot is immutable.

Do not modify the snapshot to reflect post-archive administrative transitions.

## 12. Post-Archive State

Only after the archive has been created and verified, update the active `TASK_STATE.md` to reflect the post-archive state:

- `Closure Status = CLOSED`
- `Archive = CREATED AND VERIFIED`
- `TASK_STATE Reset = PENDING APPROVAL`

The archived snapshot remains unchanged and continues to represent the pre-archive state.

`CLOSED` means that administrative closure and archival have been completed.

`CLOSED` does not mean that `TASK_STATE.md` has been reset.

Do not report `CLOSED` before archive creation and verification.

## 13. TASK_STATE Reset

Reset is a separate operation and requires a separate explicit human approval.

Do not infer reset approval from approval to close the task or create the archive.

The reset sequence is:

1. Confirm that the archive is `CREATED AND VERIFIED`.
2. Confirm that active closure status is `CLOSED`.
3. Request explicit human approval to reset `TASK_STATE.md`.
4. Keep `TASK_STATE Reset = PENDING APPROVAL` until approval is received.
5. After approval, set `TASK_STATE Reset = APPROVED`.
6. Reset `TASK_STATE.md` to its canonical empty template.
7. Verify that the reset file matches the expected template.
8. Set `TASK_STATE Reset = COMPLETED` only after successful verification.

If reset fails:

- Do not claim that reset is complete.
- Preserve the verified archive.
- Report the failure.
- Do not modify the archived snapshot.

A reset must never erase or alter the archived historical record.

## 14. Incomplete Tasks and Administrative Closure

An incomplete task can be administratively closed when all of the following conditions are met:

- Its completion classification is explicitly `INCOMPLETE`.
- Unmet acceptance criteria are documented.
- Remaining work and known limitations are documented.
- Validation results and omissions are disclosed.
- Applicable metrics are handled according to this procedure.
- Applicable framework evaluation observations are handled.
- Required human approval has been obtained.
- No unresolved human clarification or decision blocks closure.
- All applicable archive and closure requirements are satisfied.

In this situation:

- The task remains `INCOMPLETE`.
- It must not receive a standardized completed-task metrics row.
- Its administrative closure may reach `READY` and subsequently `CLOSED`.
- Administrative closure must not be represented as technical success.

## 15. Final Closure Report

At the end of the procedure, provide a concise report containing:

### Task Completion

- Task ID.
- Completion classification.
- Acceptance criteria status.
- Remaining work or limitations, if any.
- Validation summary.

### Administrative Closure

- Closure status.
- Metrics record status.
- Framework evaluation observation status.
- Archive status.
- TASK_STATE reset status.

### Evidence and Integrity

- Persistent records written and verified.
- Archive creation and verification result.
- Any unresolved limitations or failures.

### Required Distinctions

The report must distinguish clearly between:

- Task completion and administrative closure.
- Technical validation and documentary verification.
- Archive creation and TASK_STATE reset.
- Completed tasks and incomplete tasks.
- Unknown values and genuinely inapplicable metrics.

Never report a task as completed merely because it has been administratively closed.

Never report an archive as created before verifying it.

Never report a reset as completed before verifying the canonical empty template.

## 16. Canonical Authority

This file is the canonical detailed procedure for task closure.

`WORKFLOW.md` may summarize the closure sequence, but its summary must not replace, shorten, or override this procedure.

`TASK_STATE.md` defines the active state representation and must remain consistent with this procedure.

`definitions.md` defines metric meanings and allowed values. This procedure maps task evidence to those definitions and must not redefine them.

`log.md` defines the persistent metrics and framework evaluation record structure.

When a conflict is identified, stop the affected operation, document the conflict, and obtain the required human clarification before proceeding.
