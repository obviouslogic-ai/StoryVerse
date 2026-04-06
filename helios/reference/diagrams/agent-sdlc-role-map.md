
# Agent-to-SDLC Function Role Map

> Maps the 23-agent HELIos roster to 15 SDLC and IT operations functions. Each agent is classified as either "Primary" (first-order accountable in an autonomous workflow) or "Supporting" (audit, review, enforcement, or enrichment role). This mapping validates that the HELIos agent architecture provides complete SDLC lifecycle coverage with clear accountability boundaries.

---

## 1. Role Map Diagram

```mermaid
graph LR
  subgraph "Tier 0 — Human Override"
    HAA["HAA<br/>Human Authority"]
  end

  subgraph "Tier 1 — Gate Authorities"
    RRA["RRA<br/>Release Readiness"]
    AGA["AGA<br/>Architecture Guard"]
    STMA["STMA<br/>Security & Threat"]
    ATADA["ATADA<br/>Automated Testing"]
    DSCA["DSCA<br/>Supply Chain"]
  end

  subgraph "Tier 2 — Operational"
    QMSA["QMSA<br/>Quality Metrics"]
    ORFA["ORFA<br/>Ops & Reliability"]
    DXA["DXA<br/>Developer Experience"]
    PGA["PGA<br/>Process Governance"]
    CIA["CIA<br/>Cloud Intake"]  %% NOT in canonical 20-agent roster
    RCA["RCA<br/>Request Classification"]  %% NOT in canonical 20-agent roster
    REA["REA<br/>Requirements Eng."]
    PDA["PDA<br/>Privacy & Data"]
  end

  subgraph "Tier 3 — Execution"
    PPMA["PPMA<br/>Project Mgmt"]
    CEA["CEA<br/>Code Engineering"]
    ARA["ARA<br/>Audit & Review"]
    ABE["ABE<br/>AI Bug Evaluation"]
  end

  subgraph "Support Tier"
    DMA["DMA<br/>Doc Management"]
    UIBGA["UIBGA<br/>UI/Brand Guard"]
    PIA["PIA<br/>Platform Intel"]
    SSA["SSA<br/>Status Sync"]  %% NOT in canonical 20-agent roster
    SOA["SOA<br/>SLO & Observability"]
  end

  subgraph "SDLC Functions"
    F01["Cloud Intake<br/>& Triage"]
    F02["Requirements"]
    F03["Architecture<br/>& Design"]
    F04["Implementation"]
    F05["Testing & QA"]
    F06["CI/CD &<br/>Deployment"]
    F07["Release & Change<br/>Enablement"]
    F08["Documentation<br/>& Knowledge"]
    F09["Security"]
    F10["Privacy & Data<br/>Protection"]
    F11["Compliance<br/>& Controls"]
    F12["Observability<br/>& SRE"]
    F13["Reliability &<br/>Tech Debt"]
    F14["DevEx &<br/>Enablement"]
    F15["Platform Intel<br/>& Roadmap"]
  end

  CIA -->|primary| F01
  RCA -->|primary| F01
  REA -->|primary| F02
  AGA -->|primary| F03
  CEA -->|primary| F04
  ATADA -->|primary| F05
  ATADA -->|primary| F06
  RRA -->|primary| F07
  DMA -->|primary| F08
  STMA -->|primary| F09
  PDA -->|primary| F10
  PGA -->|primary| F11
  HAA -->|primary| F11
  ORFA -->|primary| F12
  SOA -->|primary| F12
  QMSA -->|primary| F13
  DXA -->|primary| F14
  PIA -->|primary| F15
  SSA -->|support| F15
```

---

## 2. Coverage Matrix

| SDLC Function | Primary Agent(s) | Supporting Agent(s) |
|---------------|------------------|---------------------|
| Cloud intake & triage | CIA, RCA | PPMA, PGA, SSA |
| Requirements | REA | PPMA, UIBGA, AGA |
| Architecture & system design | AGA | UIBGA, STMA, DSCA |
| Implementation (coding) | CEA | ABE, ARA |
| Testing & QA | ATADA | QMSA, CEA |
| CI/CD & deployment | ATADA | DSCA, RRA |
| Release & change enablement | RRA | HAA, ATADA |
| Documentation & knowledge | DMA | PGA, PPMA |
| Security (AppSec & threat modeling) | STMA | DSCA, PDA, AGA |
| Privacy & data protection | PDA | DSCA, STMA, HAA |
| Compliance evidence & controls | PGA, HAA | ATADA, DSCA, ARA |
| Observability & SRE | ORFA, SOA | QMSA, RRA |
| Reliability feedback loop & tech debt | QMSA | ARA, DXA, ORFA |
| DevEx & enablement | DXA | PGA, CEA |
| Platform intelligence & roadmap signals | PIA | PPMA, CIA |

---

## 3. Coverage Analysis

### Full Coverage
All 15 SDLC functions have at least one primary agent. No function is unowned.

### Dual-Primary Functions
Four functions have dual primary ownership:
- **Cloud intake & triage** — CIA (intake validation) + RCA (classification/routing)
- **Compliance evidence & controls** — PGA (process governance) + HAA (human authority override)
- **Observability & SRE** — ORFA (operational response) + SOA (SLO governance)
- **CI/CD & deployment** — ATADA owns both testing AND deployment pipeline governance

### Agent Workload Distribution

| Agent Count per Tier | Primary Functions | Supporting Functions |
|----------------------|:-----------------:|:--------------------:|
| Tier 0 (1 agent) | 1 | 0 |
| Tier 1 (5 agents) | 6 | 6 |
| Tier 2 (7 agents) | 6 | 3 |
| Tier 3 (4 agents) | 2 | 4 |
| Support (5 agents) | 4 | 2 |

### Boundary Observations
- **ATADA** carries the heaviest load: primary for both Testing/QA and CI/CD, plus supporting 3 other functions
- **PDA ↔ STMA boundary** is explicit: PDA owns data governance/privacy; STMA owns application security/threat modeling
- **DSCA** supports 4 functions but is primary for none in this mapping — its primary domain (supply chain) is a cross-cutting concern embedded in CI/CD and security functions
- **SSA** has the lightest load: support role for platform intelligence only (status synchronization across tools)

---

## Related Documents

- Agent Registry: [`helios/agents/00-agent-registry.md`](../../agents/00-agent-registry.md)
- Constitution: [`helios/agents/00-constitution.md`](../../agents/00-constitution.md)
- Governance Framework: [`helios/governance/helios-governance-framework-v1.md`](../../governance/helios-governance-framework-v1.md)
