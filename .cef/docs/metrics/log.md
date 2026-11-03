# CEF Metrics Log

## 1. Purpose

This file is the append-only record of standardized task metrics and framework evaluation observations for the Copilot Engineering Framework (CEF).

Its purposes are to:

- Preserve historical task records.
- Support consistent comparison between tasks.
- Record measurable outcomes without inventing or estimating missing data.
- Support periodic evaluation of framework effectiveness.
- Maintain traceability between task evidence, metric records, and framework changes.

This file must be updated only through the canonical Close Task procedure defined in `.cef/prompts/close-task.core.md`.

## 2. Record Integrity

This log is append-only.

- Existing historical records must not be silently modified, rewritten, recalculated, or removed.
- Corrections to historical data require explicit justification and must preserve traceability to the original record.
- New records must use the standardized schema defined in this document.
- Legacy records must remain identifiable as legacy records.
- Do not convert incomplete historical information into standardized metrics by inference.
- Do not invent, estimate, or retroactively fabricate measurements.
- A missing value must be represented according to the applicable metric definition.

Historical records T-001 through T-005 predate the current standardized metric procedure. They are retained as historical evidence and must not be interpreted as fully standardized measurements.

## 3. Metric Definitions Reference

The canonical definitions, applicability rules, and interpretation guidance are maintained in:

`.cef/docs/metrics/definitions.md`

This log must remain consistent with that document.

If a metric's meaning or allowed values are unclear, consult `definitions.md` and the canonical Close Task procedure before recording a value.

## 4. Standardized Task Metrics

### 4.1 Standardized Record Schema

Each eligible completed task must receive exactly one standardized metrics record.

| Field | Description |
|---|---|
| Task ID | Unique task identifier |
| Date | Date of task closure |
| Task | Short task description |
| Outcome | Standardized task outcome |
| Acceptance 1st | Whether acceptance criteria were satisfied on the first substantive implementation attempt |
| Scope Escape | Whether implementation exceeded the agreed scope |
| Severity Predicted | Initial predicted severity |
| Severity Actual | Final assessed severity |
| Confidence Predicted | Initial confidence assessment |
| Confidence Actual | Final confidence assessment |
| Iterations | Number of substantive implementation cycles |
| Active Time (min) | Estimated or measured active task time, when supported by evidence |
| Rules Caught | Framework rules or controls that prevented or caught an issue |
| Rules Friction | Rules or controls that introduced unnecessary friction |
| Validation Summary | Concise description of validation evidence |
| Notes | Additional relevant context |

The exact standardized row format must remain consistent across entries.

### 4.2 Outcome

The standardized task metrics table records completed tasks only.

For a completed task:

- `Outcome` must be `COMPLETED`.
- Exactly one row must be appended.
- The record must be based on available task evidence.

Incomplete tasks must not receive a standardized completed-task metrics row.

For an incomplete task:

- `Metrics Record` must be `NOT APPLICABLE`.
- A framework evaluation observation may still be recorded when relevant.
- If no observation is warranted, record `NOT APPLICABLE` with a documented reason in the task closure process.

Administrative closure does not transform an incomplete task into a completed task.

### 4.3 Acceptance 1st

Record whether the task's applicable acceptance criteria were satisfied on the first substantive implementation attempt.

Use the values defined in `definitions.md`, including:

- `Y`
- `N`
- `UNKNOWN`
- `PENDING HUMAN CLARIFICATION`
- `N/A`, only when genuinely not applicable and justified.

Do not interpret the absence of a recorded first attempt as a successful first-attempt result.

### 4.4 Scope Escape

Record whether implementation exceeded the scope agreed for the task.

Use the values defined in `definitions.md`, including:

- `Y`
- `N`
- `UNKNOWN`
- `PENDING HUMAN CLARIFICATION`
- `N/A`, only when genuinely not applicable and justified.

A change explicitly approved as a scope adjustment must be evaluated according to the agreed scope, not automatically classified as scope escape.

### 4.5 Severity and Confidence

Keep predicted and actual assessments separate.

- `Severity Predicted` represents the initial prediction.
- `Severity Actual` represents the final assessment supported by evidence.
- `Confidence Predicted` represents the initial confidence.
- `Confidence Actual` represents the final confidence assessment.

Use only the categories defined in `definitions.md`.

For any of these fields:

- Use `UNKNOWN` when the value should exist but cannot be established from available evidence.
- Use `PENDING HUMAN CLARIFICATION` when a human decision or clarification is necessary.
- Use `N/A` only when the metric is genuinely inapplicable, the reason is documented, and the applicable human clarification or approval has been obtained.
- Never use `N/A` merely because a task is incomplete, evidence is missing, or impact is unknown.
- Do not infer an actual severity or confidence value from an initial prediction.

### 4.6 Iterations

Record the number of substantive implementation cycles, following the definitions in `definitions.md`.

Allowed representations:

- A non-negative integer when the count is supported by reliable evidence.
- `0` when reliable evidence establishes that no substantive implementation cycle occurred.
- `UNKNOWN` when a count should exist but cannot be established from the available evidence.
- `PENDING HUMAN CLARIFICATION` when conflicting evidence or a human decision prevents a reliable classification.
- `N/A` only when the metric is genuinely inapplicable and the reason is documented.

These values are not interchangeable:

- `0` is a known numeric result.
- `UNKNOWN` means the value cannot be established.
- `PENDING HUMAN CLARIFICATION` means a decision or clarification is required.
- `N/A` means the metric does not apply.

Do not count every conversation message, review comment, or clarification as an implementation cycle.

Do not invent or estimate a cycle count.

### 4.7 Active Time

Record active task time in minutes only when it can be reasonably established from available evidence.

Allowed representations:

- A non-negative numeric value when supported by evidence.
- `UNKNOWN` when active time should have been recorded but cannot be established.
- `PENDING HUMAN CLARIFICATION` when clarification is required.
- `N/A` only when active time is genuinely inapplicable and the reason is documented.

Do not use `N/A` merely because time was not recorded.

Do not present elapsed calendar time as active work time without supporting evidence.

Approximate values must be clearly supported by the task history and must follow the metric definitions.

### 4.8 Rules Caught and Rules Friction

`Rules Caught` records framework rules, instructions, or controls that demonstrably prevented, detected, or corrected an issue.

`Rules Friction` records framework rules, instructions, or controls that introduced unnecessary effort, obstruction, or process friction.

Use identifiable rule names or concise descriptions.

When no relevant rule was identified, use the representation permitted by `definitions.md`.

Do not claim that a rule caught an issue merely because it was present in the framework.

Do not classify a necessary safeguard or justified validation step as friction solely because it required additional work.

### 4.9 Validation Summary and Notes

The validation summary must describe the evidence actually obtained.

Distinguish between:

- Implementation completed.
- Validation attempted.
- Validation passed.
- Validation failed.
- Validation not performed.
- Validation blocked or pending.

Administrative closure must not be described as technical validation.

Use notes to preserve context that materially affects interpretation of the metrics.

## 5. Legacy Historical Records

The following records are retained from the exploratory phase of CEF.

They are historical records, not standardized metrics rows. Their original values and descriptions must remain intact.

### 5.1 Legacy Records

| Task ID | Task | Sev Pred | Sev Actual | Conf Pred | Conf Actual | Iterations | Active Time (min) | Acceptance 1st | Scope Escape | Rules Caught | Rules Friction |
|---|---|---:|---:|---:|---:|---:|---:|---|---|---|---|
| T-001 | registrationDate | H | H | M | H | 3 | 50 | N | N | engine | - |
| T-002 | Lodash | H | H | M | H | 2 | ~20 | N | N | G1, G2, Red-Team | - |
| T-003 | React List | L | L | M | H | 2 | 15 | N | N | react.instructions, red-team | - |
| T-004 | Student search by name | L | L | H | H | 1 | 15 | N | N | react.instructions, red-team | - |
| T-005 | Case-insensitive student search | L | L | H | H | 2 | 20 | N | N | react.instructions, red-team | - |

### 5.2 Legacy Interpretation

These records preserve the original exploratory observations.

- `H`, `M`, and `L` are retained as originally recorded.
- Approximate values such as `~20` remain approximate.
- The original task descriptions and rule references are retained.
- The legacy records must not be silently converted into the current standardized schema.
- The historical records do not establish that the current framework has been operationally validated.
- T-001 was manually completed during the first framework test and must remain identifiable as an early exploratory record.
- The historical data may inform future evaluation, but comparisons must account for differences in methodology and recording standards.

### 5.3 Historical Integrity

T-001 through T-005 are preserved as the historical baseline.

Any future correction must:

1. Identify the affected task ID.
2. Explain the reason for the correction.
3. Preserve traceability to the original information.
4. Avoid silently rewriting the historical record.
5. Be consistent with the applicable approval requirements.

## 6. Framework Evaluation Observations

Framework evaluation observations are distinct from standardized task metrics.

They may be recorded when a task reveals relevant information about:

- Missing or ambiguous instructions.
- Rules that successfully prevented or detected errors.
- Unnecessary process friction.
- Repeated clarification needs.
- Validation weaknesses.
- Workflow inconsistencies.
- Opportunities to improve framework reliability.
- Differences between expected and observed Copilot behavior.

An incomplete task may still generate a framework evaluation observation.

An observation must be evidence-based and must not be presented as a completed-task metrics record.

### 6.1 Observation Record

Use the following structure for new observations:

| Field | Description |
|---|---|
| Observation ID | Unique identifier |
| Date | Date of observation |
| Task ID | Related task identifier |
| Category | Observation category |
| Evidence | Observable evidence supporting the observation |
| Impact | Actual or potential effect |
| Recommendation | Proposed framework improvement |
| Status | Current evaluation status |

Do not invent an observation ID or claim that a recommendation has been implemented when it has not.

## 7. Appending New Records

New records must be appended only through the canonical Close Task procedure in:

`.cef/prompts/close-task.core.md`

Before appending:

1. Confirm the task's completion classification.
2. Confirm that the Task ID is unique.
3. Confirm that the evidence supports each metric value.
4. Resolve required human clarifications.
5. Obtain the required human approval.
6. Determine whether a standardized metrics record is applicable.
7. Determine whether a framework evaluation observation is applicable.
8. Verify that the record does not duplicate an existing entry.

For a completed task:

- Append exactly one standardized metrics row.
- Set `Outcome` to `COMPLETED`.
- Do not add a second standardized row for the same Task ID.

For an incomplete task:

- Do not append a completed-task metrics row.
- Set `Metrics Record` to `NOT APPLICABLE`.
- Append a framework evaluation observation only when relevant and supported by evidence.
- If no observation is applicable, document the reason for `NOT APPLICABLE` in the closure record.

After writing, verify the appended record against the source evidence and the approved closure data.

Do not report a record as written and verified until the persisted content has been checked.

## 8. Periodic Framework Review

Periodic reviews should evaluate whether the framework is improving task execution without introducing disproportionate process overhead.

Review, when sufficient evidence is available:

- Active time trends.
- Iteration counts.
- First-attempt acceptance.
- Scope escape.
- Severity prediction versus actual severity.
- Confidence prediction versus actual confidence.
- Rules caught.
- Rules friction.
- Repeated framework observations.
- Validation quality and consistency.

### 8.1 Interpretation Requirements

- Do not draw conclusions from a small or methodologically inconsistent sample without stating the limitation.
- Do not treat missing data as a positive outcome.
- Do not treat incomplete tasks as completed tasks.
- Do not compare legacy and standardized records as if they were collected under identical procedures.
- Separate measured results from qualitative observations.
- Distinguish correlation from causation.
- Document the evidence and limitations supporting each conclusion.

### 8.2 Framework Evaluation Records

A periodic framework evaluation must identify:

- Review date.
- Records and period considered.
- Relevant trends.
- Limitations and missing evidence.
- Findings.
- Proposed changes.
- Human approval status.
- Follow-up status.

Framework changes must follow the applicable project workflow and approval requirements.

## 9. Change Control

This file is part of the CEF documentation baseline.

Changes to metric definitions must first be evaluated against `.cef/docs/metrics/definitions.md`.

Changes to the canonical closure process must be evaluated against `.cef/prompts/close-task.core.md`.

Historical records must remain protected.

Any approved change to this log must preserve consistency across the framework documentation and must not silently redefine previously recorded data.
