# Release-Delta Evaluation Gate

## Purpose

Prevent silent regressions caused by upstream platform/model/provider changes.

## Trigger Sources

- model version changes (OpenAI, Anthropic, other providers)
- platform/runtime updates (CLI handoff behavior, tool invocation semantics)
- dependency major/minor updates in core execution path
- infrastructure incident classes that change failure assumptions

## Gate Policy

No promotion to production when release-delta evaluation is stale or failing.

## Required Inputs

1. Release delta record with date, source, and impacted domains.
2. Evaluation corpus (deterministic prompts/tests and expected outcomes).
3. Baseline metric snapshot for quality, latency, and cost.
4. Fallback policy for degraded provider behavior.

## Evaluation Procedure

1. Run corpus against baseline and candidate runtime.
2. Compare:
   - task success rate
   - policy/compliance violation rate
   - retry amplification and tool-call error rate
   - median and p95 latency
   - cost per successful outcome
3. Classify result:
   - **pass**: within thresholds
   - **warn**: acceptable but needs mitigation and tracking
   - **fail**: exceeds thresholds, block promotion

## Threshold Template

| Metric | Default Threshold | Gate Action |
|-------|-------------------|-------------|
| Success rate drop | > 2% absolute | Fail |
| Compliance violation increase | > 0 | Fail |
| p95 latency regression | > 20% | Warn/Fail by severity |
| Cost per successful task increase | > 15% | Warn |
| Tool-call error rate increase | > 1% absolute | Fail |

## Audit Artifacts

- evaluation report (input set, runtime versions, metrics)
- exception record for any override
- assigned remediation with due date
