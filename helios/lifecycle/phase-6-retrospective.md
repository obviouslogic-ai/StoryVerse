# Phase 6: Retrospective and Continuous Improvement

## Goal

Evaluate pipeline effectiveness, agent performance, quality trends, and compliance posture. Feed improvements back into the system so the pipeline gets better over time.

## Cadence

| Type | Frequency | Duration | Scope |
|------|-----------|----------|-------|
| Mini-retro | Monthly | 1 hour | Last month's metrics, quick wins |
| Full retro | Quarterly | Half day | Deep analysis, pipeline evolution |

## Active Agents

| Agent | Role in Phase 6 |
|-------|-----------------|
| Project Manager (PPMA) | Facilitates retro, tracks action items |
| Quality Metrics Agent (QMSA) | Provides quality trend data |
| Document Manager (DMA) | Provides doc freshness metrics |
| Developer Experience Agent (DXA) | Provides DX friction data |
| Human Approval Authority (HAA) | Makes strategic improvement decisions |

---

## What to Review

### 1. Pipeline Effectiveness

- **Cycle time**: Average time from Specify to Validate
- **Gate pass rate**: Percentage of PRs that pass gates on first attempt
- **CI reliability**: Flaky test rate, CI uptime, average execution time
- **Deployment frequency**: How often are we shipping?
- **Rollback rate**: How often do deployments get rolled back?
- **Drill quality**: Failover/chaos drill pass rate and mean recovery time

### 2. Agent Performance

- **Review quality**: Are agent reviews catching real issues?
- **False positive rate**: Are agents blocking PRs unnecessarily?
- **Response time**: How quickly do agent gates complete?
- **Coverage gaps**: Are there areas agents miss consistently?
- **Codex batch success rate**: Percentage of Codex tasks that pass gates without rework

### 3. Quality Trends

- **QUALITY_SCORE.md trajectory**: Are grades improving, stable, or declining?
- **Tech debt trend**: Is debt growing or shrinking?
- **Test coverage trend**: Is coverage expanding?
- **Bug escape rate**: How many bugs reach production?
- **Error budget consumption**: Are SLOs being met?

### 4. Compliance Posture

- **Manifest coverage**: Are all relevant domains manifested?
- **Gate catch rate**: How often does the compliance gate catch real violations?
- **Policy drift**: Are policies up to date with current regulations?
- **Audit readiness**: Could we pass an audit today?

---

## Mini-Retro Process (Monthly)

1. **Gather metrics** (PPMA, 15 min)
   - Pull cycle time, gate pass rate, quality scores from the last 30 days
   - Compile agent performance summary
2. **Identify outliers** (PPMA + HAA, 15 min)
   - What took too long?
   - What failed unexpectedly?
   - What worked better than expected?
3. **Quick wins** (all, 15 min)
   - Identify 1–3 improvements that can be made this week
   - Create Linear issues for each
4. **Update pipeline config** (PPMA, 15 min)
   - Adjust thresholds, rules, or agent configs based on findings
   - Commit changes to `helios/` configuration

## Full Retro Process (Quarterly)

1. **Data collection** (1 hour, async before retro)
   - QMSA: Quality trend report
   - DMA: Doc freshness report
   - DXA: DX friction report
   - PPMA: Velocity and cycle time report
2. **Pipeline review** (1 hour)
   - Walk through each phase (0–5) — what's working, what isn't
   - Review agent roles — any gaps, overlaps, or inefficiencies?
   - Evaluate tooling — are MCP servers, CI, integrations serving us well?
3. **Strategic decisions** (1 hour)
   - Should we add/remove/modify agents?
   - Should we change phase durations or cadences?
   - Are compliance policies still appropriate?
   - What new capabilities would accelerate the team?
4. **Action items** (30 min)
   - Create improvement backlog items in Linear
   - Assign owners and timelines
   - Schedule pipeline config updates

---

## Output

Every retrospective produces:

| Output | Destination | Owner |
|--------|-------------|-------|
| Improvement backlog items | Linear (tagged `pipeline-improvement`) | PPMA |
| Pipeline config updates | `helios/` directory (committed to repo) | PPMA |
| Updated agent configurations | `AGENTS.md` or agent-specific configs | PPMA |
| Quality trend summary | `docs/retro/YYYY-MM-retro.md` | QMSA |
| Decision records | `docs/adr/` (if architectural changes) | AGA |

## Retro Anti-Patterns

Avoid these common retrospective failures:
- **No metrics**: Retros based on feelings instead of data
- **No action items**: Discussion without commitments
- **No follow-through**: Action items that never get done (track in Linear)
- **Blame focus**: Retros should improve the system, not judge individuals
- **Scope creep**: Retros should produce small, concrete improvements — not rewrite the pipeline

## Phase 6 Checklist

### Monthly Mini-Retro
- [ ] Metrics gathered for the past 30 days
- [ ] Outliers identified and discussed
- [ ] 1–3 quick-win improvements identified
- [ ] Linear issues created for improvements
- [ ] Pipeline config updated if needed

### Quarterly Full Retro
- [ ] All agent reports collected
- [ ] Each pipeline phase reviewed
- [ ] Strategic decisions documented
- [ ] Improvement backlog items in Linear
- [ ] Pipeline config changes committed
- [ ] Retro summary written to `docs/retro/`

## Cross-References

- Quality management: `lifecycle/phase-4-quality-entropy.md`
- Release process: `lifecycle/phase-5-testing-iteration.md`
- Development loop: `lifecycle/development-loop.md`
- Architecture decisions: `docs/adr/`
- Pilot hardening: `reference/operations/pilot-and-hardening-runbook.md`
