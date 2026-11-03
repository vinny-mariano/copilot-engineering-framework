# CEF — Periodic Framework Review

## PURPOSE

Evaluate CEF performance using standardized completed-task metrics and approved framework evaluation observations.

This document defines the review template and interpretation rules.

Metric meanings and calculation eligibility are governed by `.cef/docs/metrics/definitions.md`.

## GENERAL REVIEW RULES

1. Use standardized metrics records as the primary population for quantitative task metrics.
2. Keep incomplete-task observations separate from completed-task metrics.
3. Keep legacy records separate unless a documented methodological review establishes comparability.
4. Identify the eligible population for every calculation.
5. Report excluded and unevaluable records.
6. Do not interpret missing data as a negative result.
7. Do not calculate percentages or statistical summaries when the eligible sample is empty.
8. Identify limitations that materially affect the conclusions.
9. Do not infer causation from correlation or a small number of observations.

If a calculation has no eligible records, report `NOT CALCULABLE` and explain why.

---

# 1. REVIEW IDENTIFICATION

Review Period:

Review Date:

CEF Version:

Reviewer:

Included Task IDs:

Excluded Task IDs:

Exclusion Reasons:

Data Source:

Data Quality Limitations:

## Data population

Report separately:

- Completed tasks with standardized metrics.
- Incomplete tasks with approved framework evaluation observations.
- Legacy historical records.
- Records excluded because of missing, ambiguous or disputed information.

Do not combine these populations without explicitly identifying their different collection methods.

Identify the number of records in each population.

---

# 2. TASK OUTCOME

## Completed Tasks

Total completed tasks with standardized metrics:

Total incomplete tasks with approved framework evaluation observations:

Total framework evaluation observations:

Total legacy records reviewed:

Do not count observations as completed tasks.

Do not include legacy records in standardized task totals unless comparability has been explicitly established.

## First Pass Success

Numerator:

Number of eligible completed tasks where `acceptance_1st = Y`.

Denominator:

Number of eligible completed tasks where `acceptance_1st = Y` or `N`.

Calculation:

`First Pass Success = Numerator / Denominator × 100`

Excluded:

- N/A
- UNKNOWN
- PENDING HUMAN CLARIFICATION

Report:

- Number of eligible tasks.
- Number of excluded tasks.
- Exclusion reasons.
- Whether the result is calculable.

If the denominator is zero, report `NOT CALCULABLE`.

Do not interpret an unavailable result as 0% success.

## Scope Escape

Numerator:

Number of eligible completed tasks where `scope_escape = Y`.

Denominator:

Number of eligible completed tasks where `scope_escape = Y` or `N`.

Calculation:

`Scope Escape Rate = Numerator / Denominator × 100`

Excluded:

- N/A
- UNKNOWN
- PENDING HUMAN CLARIFICATION

Report:

- Number of eligible tasks.
- Number of excluded tasks.
- Exclusion reasons.
- Whether the result is calculable.

If the denominator is zero, report `NOT CALCULABLE`.

An approved scope change is not a scope escape.

Do not interpret an unavailable result as 0% scope escape.

---

# 3. EXECUTION EFFICIENCY

## Iterations

Eligible task count:

Median iterations:

Minimum:

Maximum:

Excluded records:

Use only established numeric values supported by task history or reliable execution evidence.

Exclude UNKNOWN and PENDING HUMAN CLARIFICATION values.

Report the number of excluded records and their reasons.

Do not invent or estimate iteration counts to complete missing records.

If no eligible numeric values exist, report `NOT CALCULABLE`.

Do not combine iteration counts with different counting methodologies without explicitly identifying the difference.

## Active Time

Eligible measured task count:

Median measured active time:

Minimum measured active time:

Maximum measured active time:

Eligible estimated task count:

Median estimated active time:

Minimum estimated active time:

Maximum estimated active time:

Excluded records:

Use `time_min` values only when their measurement type is identified.

Report measured and estimated time separately.

Do not combine estimates and measurements without an explicitly disclosed and justified methodology.

Exclude UNKNOWN, PENDING HUMAN CLARIFICATION and N/A values from numerical summaries.

Report the number of excluded records and their reasons.

If a population has no eligible values, report `NOT CALCULABLE` for that population.

Do not interpret unavailable time data as zero minutes.

---

# 4. CALIBRATION

## Severity Accuracy

Eligible comparisons:

Number of matches:

Number of mismatches:

Number of unevaluable records:

Excluded N/A records, if applicable:

Calculation:

`Severity Accuracy = Matches / Eligible Comparisons × 100`

A comparison is eligible only when both `sev_pred` and `sev_actual` are established severity classifications.

Exclude:

- UNKNOWN
- PENDING HUMAN CLARIFICATION
- N/A, if applicable

If no eligible comparisons exist, report `NOT CALCULABLE`.

## Confidence Accuracy

Eligible comparisons:

Number of matches:

Number of mismatches:

Number of unevaluable records:

Excluded N/A records, if applicable:

Calculation:

`Confidence Accuracy = Matches / Eligible Comparisons × 100`

A comparison is eligible only when both `conf_pred` and `conf_actual` are established confidence classifications.

Exclude:

- UNKNOWN
- PENDING HUMAN CLARIFICATION
- N/A, if applicable

If no eligible comparisons exist, report `NOT CALCULABLE`.

Do not combine severity and confidence accuracy into a single score.

## Calibration Analysis

Identify:

- Repeated overestimation patterns.
- Repeated underestimation patterns.
- Cases where confidence changed after investigation.
- Cases where insufficient evidence prevented evaluation.
- Differences between initial predictions and final assessments.

Do not treat a change in confidence as automatically indicating an incorrect initial assessment.

Do not infer a general calibration pattern from a small or unrepresentative sample.

---

# 5. FRAMEWORK FEEDBACK

## Rules Caught

Most frequently activated rules:

Concrete problems prevented or detected:

Evidence:

Number of eligible observations:

Identify rules that demonstrably prevented, detected or corrected concrete problems.

Do not count rules merely read, mentioned or applied without a demonstrable result.

Distinguish NONE CONFIRMED from UNKNOWN.

## Rules Friction

Most frequently reported friction:

Repeated clarification or unnecessary work:

Evidence:

Number of eligible observations:

Identify the rule, observed friction, supporting evidence and whether the friction was resolved.

Do not classify necessary safety controls or justified approval procedures as unnecessary friction.

Distinguish NONE OBSERVED from UNKNOWN.

## Unused Rules

Applicable rules not exercised during the review period:

Potential candidates for further investigation:

Do not recommend removing a rule solely because it was unused in this review period.

Distinguish applicable but unused rules from rules that were not applicable to the reviewed tasks.

---

# 6. VALIDATION QUALITY

Validation patterns:

Recurring test failures:

Acceptance criteria frequently missed:

Unverified acceptance criteria:

Verification limitations:

Red Team findings:

Evidence:

Distinguish:

- Tests planned.
- Tests actually executed.
- Tests passed.
- Tests failed.
- Tests not executed.
- Acceptance criteria not verified.

Do not treat missing validation evidence as proof of successful validation.

Do not infer a recurring defect from a single occurrence.

---

# 7. LEGACY DATA

Legacy records reviewed:

Historical limitations:

Comparability with standardized records:

Methodological justification, if applicable:

Do not include legacy records in standardized metric calculations unless a documented methodological review establishes that the comparison is valid.

T-001 must remain identified as an experimental historical record from the initial CEF test.

Do not silently normalize legacy values to the current definitions.

Do not retrospectively reinterpret historical values merely to increase the standardized sample size.

---

# 8. OBSERVATIONS

## What worked well?

Evidence:

## What generated measurable value?

Evidence:

## What generated friction?

Evidence:

## What remains uncertain?

Evidence:

## What changed compared with the previous review?

Evidence:

Distinguish direct evidence from interpretations and hypotheses.

---

# 9. DECISIONS

Decision:

Rationale:

Supporting Evidence:

Expected Impact:

Required Changes:

Approval:

Review Owner:

Decision Date:

Follow-up Review:

Possible decisions:

- KEEP — No change justified by current evidence.
- INVESTIGATE — More evidence is needed.
- ADJUST — A specific rule or procedure should be revised.
- FIX — A confirmed framework defect requires correction.
- DEFER — Decision postponed for a documented reason.

Do not use task count alone as a reason to freeze or modify the framework.

Do not treat an analytical recommendation as an approved framework change.

Obtain explicit human approval for changes requiring human authorization under `.cef/ENGINE.md`.

---

# 10. REVIEW CONCLUSION

Overall Assessment:

Main Strengths:

Main Weaknesses:

Critical Risks:

Confidence in Conclusions:

Limitations:

Eligible Standardized Task Count:

Unevaluable Record Count:

Next Review Date:
