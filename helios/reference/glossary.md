# HELIos Glossary

## Pipeline Terminology
| Term | Definition |
|------|-----------|
| Agent | An AI system with a defined role, authority, and set of responsibilities in the pipeline |
| authority tier | The hierarchical level of an agent (0-3 + Support). Do NOT confuse with "autonomy tier" (ABE A/B/C) or "autonomy control level" (UIBGA 0-3). |
| autonomy control level | UIBGA-specific mode (0=LOCKED, 1=CONSTRAINED, 2=GUIDED, 3=OPEN). Do NOT confuse with "authority tier". |
| autonomy tier | ABE-specific classification (A/B/C). Do NOT confuse with "authority tier". |
| burn rate | Rate of error budget consumption. Levels: Normal (1x), Warning (2x), Critical (5x), Emergency (10x+). |
| Constitution | The binding governance document that defines agent hierarchy, rules, and interaction protocols |
| Cortex | Predecessor system to HELIos. Referenced historically. |
| Development Loop | The 6-step cycle: Specify → Task → Execute → Gate → Merge → Validate |
| DORA metrics | Deployment Frequency, Lead Time, Change Failure Rate, MTTR. |
| Enforcement Manifest | A YAML file extracting machine-parsable rules from markdown compliance policies |
| entropy | System-level quality decay over time. Managed via doc gardening, tech debt tracking, dependency scanning. |
| error budget | Allowed failure margin = 1 - SLO Target. States: Normal (>50%), Caution (20-50%), Critical (0-20%), Exhausted (0%). |
| Executive Sponsor | The CTO for ObviousLogic.ai projects. Use "Executive Sponsor (CTO)" consistently. Equivalent to HAA in the agent layer. |
| Gate | A checkpoint where work must pass validation before proceeding. Always qualify -- "CI gate", "phase gate", "release gate", "quality gate". Never use unqualified "gate". |
| golden signals | Four observability signals (Latency, Traffic, Errors, Saturation) per Google SRE. |
| HELIos | The AI-powered development pipeline operating system |
| pipeline | The end-to-end development workflow. Always qualify -- "HELIos pipeline", "CI/CD pipeline". Never unqualified. |
| requirement trace ID | REQ-{project}-{seq} format. Assigned by REA. Do NOT confuse with "request trace ID" (UUID). |
| request trace ID | UUID for distributed tracing (trace_id). Used by ORFA. Do NOT confuse with "requirement trace ID". |
| Scoped Domain | A code area where enforcement manifests must be consulted (auth, data, encryption, logging) |
| Self-Review Loop | Process where an agent reviews its own output against AGENTS.md before opening a PR |
| severity | 4-level scale: Critical, High, Medium, Low. DXA maps S1=Critical, S2=High, S3=Medium, S4=Low. |
| Stop Condition | A defined circumstance where an agent must halt and escalate rather than proceed |
| System of Record | The authoritative source for information (repo for agents, Notion/Linear for humans) |
| tier | A classification level. Always qualify -- "authority tier", "autonomy tier", "subscription tier". Never unqualified. |
| traceability matrix | REA's requirements-to-implementation mapping artifact. |

## Agent Abbreviations
| Abbr | Full Name | Tier |
|------|-----------|------|
| ABE | AI Bug Evaluation Agent | 3 |
| AGA | Architecture Guardian Agent | 1 |
| ARA | Autonomous Refactor Agent | 3 |
| ATADA | Autonomous Test Architect & Deployment Agent | 1 |
| CEA | Coding Execution Agent | 3 |
| DMA | Document Manager Agent | Support |
| DSCA | Dependency & Supply Chain Agent | 1 |
| DXA | Developer Experience Agent | 2 |
| HAA | Human Approval Authority | 0 |
| ORFA | Observability & Runtime Feedback Agent | 2 |
| PDA | Privacy & Data Protection Agent | 2 |
| PGA | Process Governance Analyst | 2 |
| PIA | Platform Intelligence Agent | 2 |
| PPMA | Premiere Project Manager Agent | 3 |
| QMSA | Quality Metrics & SLO Agent | 2 |
| REA | Requirements Engineering Agent | 2 |
| RRA | Release Readiness Agent | 1 |
| SOA | SLO & Observability Agent | Support |
| STMA | Security & Threat Modeling Agent | 1 |
| UIBGA | UX/UI/Brand Governor Agent | Support |

## Platform Names
| Platform | Role |
|----------|------|
| Cursor | Interactive AI development environment |
| Codex | OpenAI's async code generation and review platform |
| GitHub | Source control, CI/CD, PR workflow |
| Linear | Issue tracking, sprint management |
| Notion | Knowledge base, client portal, changelog |
| Lovable | UI/UX prototyping |
| Vercel | Production deployment and edge runtime |
| Supabase | Database, auth, edge functions, storage |
| Claude | Anthropic's AI model (Opus for architecture, Sonnet for runtime) |

## Compliance Terms
| Term | Definition |
|------|-----------|
| ADR | Architecture Decision Record |
| CAIQ v4.1.0 | Cloud Security Alliance Consensus Assessments Initiative Questionnaire. |
| HIPAA | Health Insurance Portability and Accountability Act -- PHI protection requirements |
| MCP | Model Context Protocol (Cursor's server integration system) |
| MTTR | Mean Time to Restore. One of four DORA metrics. |
| MTTD | Mean Time to Detect |
| NIST SP 800-53 | Security and privacy controls catalog. Always include "SP" prefix. |
| OSCAL | Open Security Controls Assessment Language. |
| PHI | Protected Health Information |
| PII | Personally Identifiable Information |
| RLS | Row Level Security (Supabase database-level access control) |
| SBOM | Software Bill of Materials. Generated by DSCA in SPDX or CycloneDX format. |
| SLO | Service Level Objective |
| SLSA | Supply-chain Levels for Software Artifacts. |
| SOC2 | Service Organization Control 2 -- security, availability, processing integrity, confidentiality, privacy |
| STRIDE | Spoofing, Tampering, Repudiation, Information Disclosure, DoS, Elevation of Privilege. Used by STMA. |
| WCAG | Web Content Accessibility Guidelines. Used by UIBGA. |

## Verdict Terms
| Term | Meaning |
|------|---------|
| GO | All gates passed, safe to merge and deploy |
| HOLD | Issues identified but resolvable, remediation list provided |
| BLOCK | Unacceptable risk, requires HAA override to proceed |
| STOP | Agent halts due to ambiguity or constraint violation (success condition) |
