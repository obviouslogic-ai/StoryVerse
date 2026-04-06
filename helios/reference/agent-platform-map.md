# Agent-Platform Map

Visual and tabular reference of which agents operate on which platforms.

## Matrix View

```
                    Cursor  Codex  GitHub  Linear  Notion  Lovable  Vercel  Supabase
HAA                                  ●
RRA                                  ●
AGA                   ●       ●
STMA                  ●       ●
ATADA                         ●      ●
DSCA                          ●      ●
QMSA                                ●
ORFA                                                                 ●       ●
DXA                   ●
PPMA                  ●                      ●       ●
CEA                   ●       ●
ARA                           ●
DMA                           ●                      ●
UIBGA                 ●                                      ●
```

## By Platform

### Cursor (Interactive Development)
Active agents: AGA, STMA, DXA, PPMA, CEA, UIBGA
Config: .cursor/rules/*.mdc (5 files)
MCP servers: Supabase, GitHub, Notion, Linear, Browser

### Codex (Async/Batch)
Active agents: AGA, STMA, ATADA, DSCA, CEA, ARA, DMA
Config: AGENTS.md (under 100 lines, table of contents for agents)

### GitHub (Enforcement Layer)
Active agents: HAA, RRA, ATADA, DSCA, QMSA
Config: .github/workflows/*.yml (4 files), branch protection, Dependabot

### Linear (Work Tracking)
Active agents: PPMA
Config: Issue templates, labels, sprint settings

### Notion (Knowledge Base)
Active agents: PPMA, DMA
Config: Database schemas, automation triggers

### Lovable (Prototyping)
Active agents: UIBGA
Rule: Exploration only. Refactor to architecture before merge.

### Vercel (Deployment)
Active agents: ORFA
Config: Auto-deploy on main, preview deployments on PRs

### Supabase (Data Platform)
Active agents: ORFA
Config: RLS policies, auth settings, edge functions, migrations

## Configuration File Summary

| Config File | Platform | Agents Implementing |
|-------------|----------|-------------------|
| helios-governance.mdc | Cursor | All (constitutional rules) |
| coding-conventions.mdc | Cursor | DXA, CEA |
| architecture-rules.mdc | Cursor | AGA |
| security-rules.mdc | Cursor | STMA |
| compliance-enforcement.mdc | Cursor | STMA, CEA |
| AGENTS.md | Codex | AGA, STMA, CEA, ARA, DMA |
| ci.yml | GitHub Actions | RRA, ATADA, QMSA |
| codex-review.yml | GitHub Actions | ATADA |
| compliance-gate.yml | GitHub Actions | RRA, ATADA |
| notion-changelog.yml | GitHub Actions | DMA |
