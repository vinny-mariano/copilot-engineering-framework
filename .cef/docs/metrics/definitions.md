# CEF — Metrics Definitions

## PURPOSE

Define the operational meaning, evidence requirements and recording rules for all CEF metrics.

This document is the canonical reference for metric collection, task outcome classification and periodic framework evaluation.

The purpose of metrics is to evaluate both task outcomes and framework behavior without introducing fabricated measurements or misleading conclusions.

## GOVERNING PRINCIPLES

1. Evidence takes precedence over estimates.
2. Metrics must be derived from available records whenever possible.
3. The human should not be asked to manually reconstruct information already present in the repository or task history.
4. The agent must not invent missing measurements.
5. Unknown values must remain explicitly unknown.
6. Historical records must not be silently corrected or overwritten.
7. Incomplete tasks may provide framework evaluation evidence without being counted as completed tasks.
8. Metric definitions must remain consistent across tasks and review periods.
9. A metric must not be assigned a value merely to make a record appear complete.
10. The same evidence and value-state conventions must be used during collection, closure and periodic review.
11. Task completion, administrative closure and framework evaluation must remain distinct classifications.
12. A successfully closed task is not necessarily a completed implementation task.

## VALUE STATES

Use the following conventions:

| Value | Meaning |
|---|---|
| Measured | Established through reliable evidence or a documented measurement. |
| Estimated | Approximation based on available evidence. Must be explicitly identified. |
| UNKNOWN | The value cannot be established from available evidence. |
| PENDING HUMAN CLARIFICATION | The definition, interpretation, conflicting evidence or required decision needs human clarification. |
| N/A | The metric does not apply to the task. |

Distinguish carefully:

- `UNKNOWN` means the available evidence is insufficient.
- `PENDING HUMAN CLARIFICATION` means a human response or decision is necessary.
- `N/A` means the metric is genuinely inapplicable.

Do not use a generic `PENDING` value as a substitute for these states.

Do not replace UNKNOWN, PENDING HUMAN CLARIFICATION or N/A with numeric or categorical values merely to complete a record.

For numeric measurements:

- Use `MEASURED: value` for measured values.
- Use `ESTIMATED: value` for estimates.
- Use `UNKNOWN`, `PENDING HUMAN CLARIFICATION` or `N/A` when applicable.

For categorical measurements, use the explicitly defined categories and value states for the corresponding metric.

Do not combine measured and estimated values in the same statistical calculation unless the review explicitly presents and justifies that methodology.

---

# 1. TASK OUTCOME

## Task Completion

A task is classified as COMPLETED only when:

- Its approved objective has been achieved.
- Approved implementation work has been performed, when implementation is part of the task.
- Applicable acceptance criteria have been evaluated and satisfied.
- Required validation has been performed or explicitly identified as unavailable, where the task's acceptance criteria permit that limitation.
- Required review procedures have been completed.
- Blocking issues have been resolved.
- The task's completion criteria have been satisfied.

A task that stops during Intake, Planning, Review or an incomplete implementation attempt must not be counted as a completed task.

A task that does not require implementation may be completed through its own applicable acceptance criteria.

Completion classification must reflect the actual task objective. Do not classify an incomplete implementation as completed merely because its planning or documentation work was completed.

## Incomplete Tasks

A task is INCOMPLETE when its approved objective or one or more applicable acceptance criteria remain unsatisfied.

Incomplete tasks:

- Must not be recorded as completed implementation tasks.
- Must not receive a standardized completed-task metrics record.
- May provide valid evidence for framework evaluation.
- May receive a separate framework evaluation observation when relevant and approved.

An incomplete task may still undergo administrative closure when its incomplete status, unresolved issues and available evidence are accurately documented and no pending human decision prevents closure.

Administrative closure does not change the task's completion classification.

## Administrative Closure

Administrative closure is the completion of the documentary, archival and administrative procedures associated with a task.

It is distinct from implementation completion.

A task may therefore have:

- Task completion: COMPLETED or INCOMPLETE.
- Administrative closure: CLOSED or not yet CLOSED.

Do not use administrative closure as evidence that the implementation objective was achieved.

Follow the canonical Close Task procedure for closure, archival and reset requirements.

## Framework Evaluation

Framework behavior may be evaluated independently of task completion.

Examples include:

- Intake quality.
- Planning quality.
- Correct identification of risks.
- Approval gate behavior.
- Scope control.
- Evidence collection.
- Instruction loading.
- Verification discipline.
- Closure reliability.

An incomplete task may therefore provide valid framework evaluation evidence.

Do not mix framework evaluation counts with completed task counts.

---

# 2. CORE METRICS

## time_min

**Meaning:** Active working time spent on the task, expressed in minutes.

Include:

- Active human work directly related to the task.
- Active agent execution time when reliably measurable.
- Relevant review and verification work.

Exclude:

- Idle time.
- Time waiting for human responses.
- Unattended elapsed time.
- Model response latency when it is not part of a reliable active-time measurement.

Rules:

- Prefer measured values.
- Do not infer total working time from isolated interaction timestamps.
- Do not convert response latency into active working time.
- If the total cannot be established reliably, record UNKNOWN.
- Estimated values must be identified as estimates and must not be presented as precise measurements.
- Preserve the measurement type when transferring the value to the metrics log.

Standardized log representation:

- `MEASURED: 35`
- `ESTIMATED: 20`
- `UNKNOWN`
- `PENDING HUMAN CLARIFICATION`
- `N/A`

The examples are illustrative and do not represent actual task measurements.

Use N/A only when active working time is genuinely inapplicable, not merely because time was not recorded.

## iterations

**Meaning:** Number of substantive task execution cycles.

A cycle is a meaningful attempt to advance or correct the task through an interaction or sequence of related operations.

Examples:

- A planning cycle that produces a revised plan.
- An implementation cycle that produces a change.
- A corrective cycle following a failed validation.
- A review cycle that results in a substantive revision.

Do not count:

- Simple greetings.
- Repeated status messages without substantive work.
- Tool latency.
- Passive waiting.
- Multiple commands that form one continuous operation as separate iterations.

Rules:

- Count only cycles supported by task history or reliable execution evidence.
- Distinguish planning, implementation and correction cycles when the evidence allows.
- Do not assume that one conversation message equals one iteration.
- Use `0` when reliable evidence establishes that no substantive execution cycle occurred.
- Use UNKNOWN when a count should exist but cannot be reliably established.
- Use PENDING HUMAN CLARIFICATION when a human decision is necessary to determine the applicable counting method or resolve conflicting evidence.
- Use N/A only when the metric is genuinely inapplicable to the task.
- Do not invent a count to fill a missing historical record.

Zero, UNKNOWN and N/A are not interchangeable.

## acceptance_1st

**Meaning:** Indicates whether all applicable acceptance criteria were satisfied in the first evaluated implementation.

Values:

- Y — All applicable acceptance criteria passed in the first evaluated implementation.
- N — One or more applicable acceptance criteria required corrective implementation.
- N/A — No implementation was required or performed for a completed task.
- UNKNOWN — The first implementation evaluation cannot be established from available evidence.
- PENDING HUMAN CLARIFICATION — Conflicting evidence or an unresolved human decision prevents classification.

Rules:

- Base the value on the first implementation evaluation and its supporting validation evidence.
- A successful first implementation does not mean the task was free of later review findings.
- A defect discovered during Red Team Review must be reported separately.
- Do not use N merely because a task was interrupted before implementation.
- Do not classify an incomplete task as a completed task merely to assign N/A.
- Use N/A when no implementation was applicable to the completed task.
- If the first implementation evaluation cannot be established for a completed task, use UNKNOWN.
- If conflicting evidence or an unresolved human decision prevents classification, use PENDING HUMAN CLARIFICATION.

A later correction does not change the result of the first implementation evaluation.

## scope_escape

**Meaning:** Indicates whether implementation work exceeded the explicitly approved scope without the required authorization.

Values:

- Y — An unauthorized scope expansion occurred.
- N — No unauthorized scope expansion occurred.
- UNKNOWN — Available evidence is insufficient to establish the result.
- PENDING HUMAN CLARIFICATION — A conflict or decision requires human clarification.
- N/A — No implementation was performed or required for a completed task.

Rules:

- An approved scope change is not a scope escape.
- A proposed change that was not implemented is not a scope escape.
- An unrelated modification made without authorization is a scope escape.
- Distinguish scope escape from an authorized scope revision.
- Do not use N/A when implementation occurred but the evidence is insufficient.
- Do not classify an incomplete task as completed merely to assign N/A.

---

# 3. CALIBRATION METRICS

## sev_pred

**Meaning:** Severity predicted during the initial task assessment.

Allowed values:

- L — LOW
- M — MEDIUM
- H — HIGH
- C — CRITICAL
- UNKNOWN — Insufficient evidence for an initial classification.
- PENDING HUMAN CLARIFICATION — A human decision or clarification is necessary before classification.

Record the initial prediction. Do not retroactively replace it with the final classification.

Do not use PENDING as a severity category.

N/A is not a default severity prediction. If the initial assessment genuinely cannot be classified because the metric is inapplicable, document the reason and obtain human clarification before recording N/A.

## sev_actual

**Meaning:** Severity established after sufficient technical investigation of the actual implementation and its impact.

Allowed values:

- L — LOW
- M — MEDIUM
- H — HIGH
- C — CRITICAL
- UNKNOWN — Investigation remains insufficient.
- PENDING HUMAN CLARIFICATION — A human decision or clarification is necessary before classification.

Rules:

- Severity must reflect the actual affected components and operational impact.
- Do not assign a final severity solely from the wording of the original request.
- A task that lacks the target application or necessary technical context may remain UNKNOWN.
- Do not treat UNKNOWN or PENDING HUMAN CLARIFICATION as severity categories when calculating calibration accuracy.
- Do not silently convert an unresolved assessment into a severity classification.
- N/A must not be used merely because the task is incomplete or its impact is unknown.

## conf_pred

**Meaning:** Initial confidence in the technical assessment.

Allowed values:

- L — LOW
- M — MEDIUM
- H — HIGH
- UNKNOWN — The initial confidence assessment cannot be established from reliable evidence.
- PENDING HUMAN CLARIFICATION — A human decision is necessary to establish the intended assessment.

Record the initial assessment without retroactively changing it.

## conf_actual

**Meaning:** Confidence after the relevant evidence has been collected and evaluated.

Allowed values:

- L — LOW
- M — MEDIUM
- H — HIGH
- UNKNOWN — Available evidence is insufficient to establish confidence reliably.
- PENDING HUMAN CLARIFICATION — A human decision is necessary to resolve the assessment.

Rules:

- Confidence measures the strength of the available evidence supporting the assessment.
- Confidence is independent of severity.
- High severity does not automatically imply low confidence.
- Low severity does not automatically imply high confidence.
- Missing evidence must not be treated as confirmation.
- Do not retroactively rewrite the initial prediction.
- Do not assign HIGH confidence solely because an assessment appears plausible.

## Applicability of Calibration Metrics

Severity and confidence are assessment metrics, not implementation outcome labels.

When an assessment is applicable, classify it using the documented categories.

Do not use N/A simply because:

- The task was incomplete.
- The implementation failed.
- The task was administratively closed.
- The evidence needed for a reliable classification is missing.

Use UNKNOWN when evidence is insufficient.

Use PENDING HUMAN CLARIFICATION when a human decision is required.

If a metric is genuinely inapplicable, document the reason and obtain human clarification before recording N/A.

## Calibration Accuracy

For both severity and confidence, compare the initial prediction with the final established assessment.

A comparison is eligible only when both values are established.

Classification:

- MATCH — Initial prediction equals final assessment.
- MISMATCH — Initial prediction differs from final assessment.
- NOT EVALUABLE — One or both values are UNKNOWN or PENDING HUMAN CLARIFICATION.

Report:

- Number of eligible comparisons.
- Number of matches.
- Number of mismatches.
- Number of excluded or unevaluable comparisons.

Do not calculate accuracy using UNKNOWN or PENDING HUMAN CLARIFICATION cases as if they were incorrect predictions.

Do not combine severity and confidence into a single accuracy score.

Do not treat N/A as a mismatch.

---

# 4. FRAMEWORK FEEDBACK

## rules_caught

**Meaning:** CEF rules or instructions that demonstrably identified, prevented or corrected a concrete problem during the task.

Examples:

- An approval gate prevented an unauthorized operation.
- A technology-specific instruction identified a contract risk.
- A verification rule exposed a failed acceptance criterion.
- A Red Team finding identified a defect.

Rules merely read or mentioned do not count as rules caught.

Record the relevant rule identifier and supporting evidence.

If no rule demonstrably caught a problem, record `NONE CONFIRMED`.

If the evidence is insufficient to establish whether a rule caught a problem, record UNKNOWN rather than NONE CONFIRMED.

## rules_friction

**Meaning:** CEF rules or instructions that caused observable and unnecessary operational friction.

Examples:

- Conflicting instructions caused repeated clarification.
- A redundant procedure caused avoidable work.
- An unclear rule prevented a valid operation until clarification.
- A rule required repeated manual steps that could reasonably be standardized.

Do not classify necessary safety controls, legitimate approval gates or justified verification work as friction merely because they require additional effort.

Record:

- Rule identifier.
- Observed friction.
- Evidence.
- Whether the friction was resolved.

If no friction was observed, record `NONE OBSERVED`.

If the evidence is insufficient to establish whether friction occurred, record UNKNOWN rather than NONE OBSERVED.

## Unused Rules

A rule is unused in a task when it was applicable to the task but was not triggered or materially relevant during execution.

Rules that were not applicable must not be classified as unused.

Absence of activation in one task does not establish that a rule is unnecessary.

---

# 5. VALIDATION METRICS

## validation_summary

**Meaning:** Concise description of validation performed and its overall outcome.

Include:

- Tests or procedures executed.
- Relevant results.
- Important failures.
- Unverified acceptance criteria.
- Material limitations.

Rules:

- Distinguish executed tests from planned tests.
- Do not report a test as passed if it was not executed.
- Include relevant evidence or references when available.
- Do not replace detailed validation evidence with a vague statement such as "tests passed".
- Identify unavailable validation explicitly.
- Do not interpret the absence of reported errors as proof of successful validation.
- Do not use a successful administrative closure as evidence of successful technical validation.

---

# 6. LOGGING RULES

Each completed task must have one canonical standardized metrics record.

For standardized records:

- `Outcome` must be `COMPLETED`.
- The Task ID must be unique across the complete log, including historical legacy records.
- Each metric must follow the definitions in this document.
- Measurement types must remain explicit.
- Unknown and not-applicable values must remain distinguishable.
- Incomplete tasks must not receive a completed-task metrics record.

The canonical metrics log is append-only.

Before appending:

1. Establish the Task ID from reliable evidence.
2. Check for an existing Task ID.
3. Consolidate the available task-state and validation evidence.
4. Identify missing, ambiguous or conflicting information.
5. Prepare one proposed metrics record.
6. Present the record to the human.
7. Obtain explicit approval.
8. Append the approved record to the standardized section.
9. Verify the resulting log.

Never overwrite an existing record silently.

If a Task ID already exists, stop and request a decision before taking any action that could affect the historical record.

Incomplete tasks may be documented as framework evaluations, but must not be presented as completed tasks.

Legacy historical records must remain unchanged unless a specific evidence-based correction is explicitly approved.

---

# 7. PERIODIC REVIEW RULES

Periodic reviews must use the definitions in this document.

For each indicator:

- Identify the review period.
- Identify the included tasks.
- State the numerator and denominator when applicable.
- Exclude N/A, UNKNOWN and PENDING HUMAN CLARIFICATION values from calculations where appropriate.
- Report the number of excluded or unevaluable records.
- Distinguish measured values from estimates.
- Avoid drawing conclusions from insufficient samples.

For `acceptance_1st`, calculate first-pass success using only Y and N values.

For `scope_escape`, calculate the scope escape rate using only Y and N values.

For calibration accuracy, use only eligible comparisons where both values are established.

For time-based statistics:

- Report measured and estimated values separately.
- Do not combine them without an explicitly justified methodology.
- Identify the eligible sample count.
- Exclude UNKNOWN and PENDING HUMAN CLARIFICATION values.
- Exclude N/A values because the metric is inapplicable.

For iteration statistics:

- Use numeric counts, including zero when supported by evidence.
- Exclude UNKNOWN and PENDING HUMAN CLARIFICATION values.
- Exclude N/A values because the metric is inapplicable.
- Identify the eligible sample count.

For `rules_caught` and `rules_friction`:

- Distinguish confirmed rule identifiers from `NONE CONFIRMED` and `NONE OBSERVED`.
- Do not treat UNKNOWN as an absence of events.
- Identify the number of records with insufficient evidence.

Do not infer causation from correlation or a small number of observations.

Do not treat a single task as proof of general framework effectiveness.

Do not compare review periods as if their populations were equivalent when their data quality or inclusion criteria differ materially.

---

# 8. HISTORICAL DATA INTEGRITY

Historical records created before these definitions were adopted may contain incomplete, ambiguous or inconsistent values.

Rules:

1. Preserve original records.
2. Do not silently rewrite historical metrics to fit the new definitions.
3. Identify inconsistencies in a separate audit note.
4. Do not infer missing values from unrelated records.
5. Distinguish historical experimental data from standardized records collected under the current definitions.
6. Apply the current definitions prospectively unless an explicit, evidence-based historical correction is approved.

T-001 is an experimental historical record from the initial CEF test.

Its manually assembled metrics must not be treated as a fully standardized measurement baseline.

Historical values must not be silently normalized to the current value states.

---

# 9. AUTHORITY

The human retains authority over:

- Approval of proposed metrics records.
- Resolution of conflicting historical evidence.
- Changes to metric definitions.
- Decisions to correct historical records.
- Interpretation of ambiguous results.

The agent is responsible for:

- Inspecting available evidence.
- Consolidating information.
- Identifying missing or conflicting values.
- Applying the documented definitions.
- Preparing proposed records.
- Verifying approved writes.

The agent must never invent measurements or silently change historical data.