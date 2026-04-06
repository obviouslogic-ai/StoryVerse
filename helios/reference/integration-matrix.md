# Integration Matrix

Platform integration reference for HELIos pipeline. Shows which platforms are used, what role they play, which agents interact with them, and what MCP or API integrations are required.

---

## Platform Integration Map

| Platform | Role in Pipeline | Primary Agents | Integration Type | Status |
|----------|-----------------|----------------|-----------------|--------|
| GitHub | Source control, CI/CD, PR workflow, branch protection | CEA, ARA, ABE, ATADA, AGA, STMA, DSCA, RRA, HAA, REA, PDA | GitHub MCP | Active |
| Linear | Issue tracking, sprint management, execution state | PPMA, CEA, ABE, PGA, REA, SOA | Linear MCP | Active |
| Notion | Knowledge base, client portal, changelog, spec management | PPMA, DMA, PGA, REA | Notion MCP | Active |
| Figma | UI/UX design, prototyping, design system governance | UIBGA | Figma MCP | Active |
| Supabase | Database, auth, edge functions, storage, RLS enforcement | CEA, STMA, ORFA, SOA, PDA | Supabase MCP | Active |
| Vercel | Production deployment, edge runtime, preview environments | CEA, ORFA, RRA, SOA | Vercel Dashboard | Active |
| Cursor | Interactive AI development, rule enforcement | AGA, STMA, DXA, PPMA, CEA, UIBGA | Cursor Rules (.mdc) | Active |
| Codex | Async/batch code generation, recurring tasks, doc gardening | CEA, ARA, ABE, ATADA, DSCA, DMA, PGA | Codex Tasks / AGENTS.md | Active |
| Slack | Team communication, notifications | ORFA (alerts) | Slack MCP | Active |
| Outlook | Email communication, calendar | PPMA (scheduling) | Outlook MCP | Active |
| Asana | Cross-functional coordination, milestones, KPIs, stakeholder visibility | PPMA (reporting) | Asana MCP | Active |

---

## System-of-Record Boundaries

| Domain | System of Record | Authoritative For |
|--------|-----------------|-------------------|
| Compliance Truth | External Compliance Platform | Regulatory status, audit trail, compliance determinations |
| Engineering Execution | Linear + GitHub | Sprint planning, PRs, code changes, CI/CD pipeline |
| Knowledge & Documentation | Notion + Repo | Specs, architecture decisions, changelogs |
| Cross-Functional Coordination | Asana | Milestones, KPIs, stakeholder visibility, department sync |

---

## MCP Server Inventory

| MCP Server | Connected Agents | Primary Operations |
|------------|-----------------|-------------------|
| GitHub MCP | AGA, STMA, ATADA, DSCA, CEA, ARA, ABE, PGA, REA, PDA | Repo inspection, PR creation, CI status, branch management |
| Linear MCP | PPMA, CEA, ABE, PGA, REA, SOA | Issue creation, state monitoring, sprint management |
| Notion MCP | PPMA, DMA, PGA, REA | Spec management, doc sync, changelog |
| Supabase MCP | CEA, STMA, ORFA, SOA, PDA | Migrations, RLS verification, logs, SLO definitions, data classification |
| Figma MCP | UIBGA | Design system governance |
| Slack MCP | ORFA | Alert notifications |
| Outlook MCP | PPMA | Calendar, scheduling |
| Asana MCP | PPMA | KPI reporting, milestone tracking |

---

## Data Flow Direction

| Flow | Direction | Mechanism |
|------|-----------|-----------|
| Linear → GitHub | Bidirectional | PPMA/CEA create branches; CI results update Linear |
| Repo → Notion | Unidirectional (doc sync) | DMA syncs code changes to Notion docs |
| Linear → Asana | Unidirectional (reporting) | PPMA pushes milestone/KPI updates |
| All Platforms → ORFA | Inbound (monitoring) | ORFA collects runtime signals |

---

## Integration Status Legend

| Status | Meaning |
|--------|---------|
| Active | MCP server connected and operational |
| Planned | Integration designed but MCP server not yet built |
| Partial | Some features connected, others pending |
