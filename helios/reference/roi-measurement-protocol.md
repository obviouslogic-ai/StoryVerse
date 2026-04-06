# ROI Measurement Protocol

## Purpose

This document defines how business value is measured, estimated, logged, and reported across the HELIos pipeline. Every agent action that produces an observable outcome must be classified by its business impact. ROI measurement is a system property -- it supplements quality enforcement but never overrides it.

**Constitutional Authority:** Constitution Section 12 (Business Value Measurement)

---

## 1. Impact Types

All agent actions are classified using one of 8 impact types:

| Impact Type | Description | Example |
|-------------|-------------|---------|
| `time_saved` | Human hours eliminated through automation | Automated report generation replacing manual compilation |
| `error_prevented` | Defects caught before reaching production | CI gate blocking a regression before merge |
| `cost_reduced` | Direct cost reduction (infrastructure, tooling, manual effort) | Optimized database queries reducing compute costs |
| `compliance_ensured` | Compliance requirements satisfied automatically | RLS policy enforcement verified without manual audit |
| `quality_improved` | Measurable improvement in code quality, test coverage, or reliability | Test coverage increase from 60% to 85% |
| `risk_mitigated` | Security, operational, or business risk reduced | Dependency vulnerability patched before exploitation |
| `knowledge_captured` | Institutional knowledge codified into documentation, tests, or automation | Architecture decision documented as ADR |
| `process_automated` | Manual process replaced with automated pipeline step | Manual deploy checklist replaced by CI gate |

### Impact Type Selection Rules

1. Choose the **primary** impact type -- the most direct value created
2. A single action may have **multiple** impact classifications (e.g., a security fix is both `risk_mitigated` and `error_prevented`)
3. When in doubt, choose the impact type that is most measurable
4. Do not inflate -- `time_saved` of 5 minutes is still valuable and should be logged honestly

---

## 2. Value Estimation

### When to Estimate

Every execution plan produced by PPMA must include a `## BUSINESS VALUE` section with:

- **Impact Type:** One of the 8 types above
- **Estimated Value:** Description of expected value + confidence level
- **Measurement Method:** How actual value will be verified post-delivery

### Estimation Methodology

#### Time Saved

```
Value = Hours Saved x Hourly Rate x Frequency
```

| Task Type | Typical Time Saved |
|-----------|-------------------|
| Manual report generation | 30-120 min per report |
| Code review preparation | 15-30 min per PR |
| Documentation update | 20-60 min per document |
| Bug investigation | 30 min - 8 hours depending on severity |
| Credential/config setup | 15 min per credential |
| Test writing | 15-45 min per test suite |

#### Error Prevented

```
Value = (Probability of Reaching Production) x (Cost of Production Incident)
```

| Severity | Estimated Production Cost |
|----------|--------------------------|
| Low (cosmetic) | 1-2 hours remediation |
| Medium (functional) | 4-8 hours remediation + user impact |
| High (data/security) | 16-40 hours remediation + incident response |
| Critical (outage) | 40+ hours + business impact |

#### Cost Reduced

```
Value = Previous Cost - New Cost (per period)
```

Track monthly or annual reduction in: compute, storage, third-party API calls, manual labor, tooling licenses.

#### Compliance Ensured

```
Value = (Audit Preparation Hours Saved) + (Risk of Non-Compliance)
```

Compliance value is measured in audit preparation time eliminated and risk reduction from automated enforcement.

### Confidence Levels

| Level | Meaning | When to Use |
|-------|---------|-------------|
| `high` | Estimate is based on measured data or direct observation | Recurring tasks with known baselines |
| `medium` | Estimate is based on reasonable assumptions | First-time tasks with comparable precedents |
| `low` | Estimate is directional only | Novel work without clear precedent |

---

## 3. Value Logging Format

### In Execution Plans (Pre-Delivery)

```markdown
## BUSINESS VALUE

- **Impact Type:** time_saved
- **Estimated Value:** Saves ~2 hours of manual testing per sprint (confidence: high)
- **Measurement Method:** Compare pre/post test execution time via CI metrics
```

### In Changelog Entries (Post-Delivery)

When recording completed work in the changelog (Notion or repo), include:

| Field | Description |
|-------|-------------|
| `ImpactType` | Primary impact classification |
| `EstimatedValue` | Pre-delivery estimate (text description) |
| `Confidence` | Estimation confidence: low / medium / high |

### In Sprint Reports (Aggregated)

QMSA aggregates per-action value data into sprint-level summaries:

```markdown
## Sprint Business Value Summary

### Value Delivered
| Impact Type | Count | Estimated Value |
|-------------|-------|-----------------|
| time_saved | 12 | ~28 hours labor |
| error_prevented | 5 | 3 production incidents avoided |
| compliance_ensured | 3 | Audit-ready for SOC 2 controls |

### Investment
- Agent execution time: X hours
- CI compute: Y minutes
- Human steering: Z hours

### Confidence Distribution
- High confidence: 60%
- Medium confidence: 30%
- Low confidence: 10%
```

---

## 4. Aggregation Rules

### Who Aggregates

- **PPMA** is responsible for **estimating** business value at planning time
- **QMSA** is responsible for **aggregating** value data into reports
- Individual agents **log** their contributions but do not self-aggregate

### Aggregation Cadence

| Period | Responsibility | Output |
|--------|---------------|--------|
| Per action | Executing agent | Value log entry in execution record |
| Per sprint | QMSA | Sprint business value summary |
| Quarterly | QMSA | Quarterly ROI report with trend analysis |

### Aggregation Principles

1. **No double-counting.** If an action has multiple impact types, the primary type is used for aggregation. Secondary impacts are noted but not summed.
2. **Recurring value compounds.** A daily automation that saves 30 min/day is logged once but its annualized value is calculated in reports.
3. **Estimates are revised.** Post-delivery actual values replace initial estimates when measured data is available.
4. **Investment includes all costs.** CI compute, agent execution time, human steering hours, and platform costs are tracked as investment.

---

## 5. Reporting

### Sprint Report (QMSA Responsibility)

Contains:
- Total estimated value by impact type
- Investment summary
- Confidence distribution
- Top 5 highest-value actions
- Trend comparison to previous sprint

### Quarterly Report (QMSA Responsibility)

Contains:
- Cumulative value by impact type
- ROI trend analysis
- Estimation accuracy (estimated vs. actual where measured)
- Recurring value forecast
- Recommendations for value optimization

### Reporting Principles

1. Reports are generated from pipeline data, not manually compiled
2. Reports flow to Notion for stakeholder visibility and to the repo for agent consumption
3. ROI data is used to **prioritize** future work, not to justify cutting corners
4. Value estimates are **directional**, not precise -- the goal is visibility and trend analysis

---

## 6. Per-Agent ROI Responsibilities

| Agent | ROI Role | What It Tracks |
|-------|----------|---------------|
| **PPMA** | Primary estimator | Includes business value in every execution plan |
| **QMSA** | Primary aggregator | Aggregates per-action data into sprint and quarterly reports |
| **CEA** | Implementation logger | Records implementation effort and time metrics |
| **ARA** | Refactoring logger | Tracks quality improvements and cost reductions from refactoring |
| **ATADA** | Error prevention logger | Tracks defects caught, regression prevented |
| **DSCA** | Risk mitigation logger | Tracks supply chain risks prevented |
| **ORFA** | Cost metrics logger | Tracks infrastructure cost trends |
| **DXA** | Efficiency logger | Tracks developer friction reduction and process automation |
| **DMA** | Knowledge logger | Tracks documentation coverage and knowledge codification |
| **RRA** | Release value summarizer | Includes value summary in release readiness reports |
| HAA | No direct ROI tracking | Reviews ROI reports for strategic alignment |
| AGA | No direct ROI tracking | Evaluates architectural decisions for cost/risk impact |
| STMA | No direct ROI tracking | Contributes to risk_mitigated through threat modeling |
| UIBGA | No direct ROI tracking | Contributes to quality_improved through design consistency |

---

## 7. Mapping to Cortex Impact Types

For projects migrating from Cortex, the following mapping applies:

| Cortex ImpactType | HELIos Impact Type |
|-------------------|-------------------|
| `REVENUE_ENABLED` | `time_saved` or `process_automated` (context-dependent) |
| `REVENUE_ACCELERATED` | `time_saved` |
| `COST_AVOIDED` | `risk_mitigated` |
| `COST_REDUCED` | `cost_reduced` |
| `TIME_SAVED` | `time_saved` |
| `PRODUCTIVITY_GAIN` | `process_automated` |
| `QUALITY_IMPROVEMENT` | `quality_improved` |
| `OPTIMIZATION` | `cost_reduced` or `quality_improved` (context-dependent) |

The HELIos impact types are pipeline-focused and project-agnostic. The Cortex types include business/revenue categories that are project-specific and should be mapped to the closest pipeline equivalent.

---

## 8. Anti-Patterns

1. **Value inflation.** Do not estimate higher than reasonable to make reports look good. Value estimates are directional, not targets.
2. **ROI-driven shortcuts.** High ROI does not justify bypassing quality gates, compliance checks, or safety invariants.
3. **Measurement overhead.** If tracking value takes more effort than the value itself, simplify the tracking. The system should be lightweight.
4. **Gaming metrics.** Splitting one task into many to inflate action counts is a compliance violation.
5. **Ignoring low-value work.** Small improvements compound. A 5-minute time saving that runs daily is worth more than a one-time 2-hour saving.
