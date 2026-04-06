# Phase 1: Knowledge Base Creation (Days 3–4)

## Goal

Build the repository knowledge base that agents need to operate. Without this, agents work blind.

## Duration

2 days

## Active Agents

| Agent | Role in Phase 1 |
|-------|-----------------|
| Project Manager (PPMA) | Guides knowledge base creation sequence |
| Architecture Guardian (AGA) | Reviews ARCHITECTURE.md for completeness |
| Security Agent (STMA) | Reviews SECURITY.md and threat model |
| Document Manager (DMA) | Ensures documentation standards are met |

## Steps

1. **Write ARCHITECTURE.md** (from `templates/ARCHITECTURE.md.template`)
   - Domain map with directory structure
   - Package layering rules
   - Dependency rules
   - Platform-specific patterns
2. **Write `docs/design-docs/core-beliefs.md`**
   - Engineering principles the team commits to
   - Quality philosophy
   - Trade-off framework
3. **Write MVP product specs** (`docs/product-specs/`)
   - At least one spec for the first feature
   - Acceptance criteria for each spec
   - Compliance considerations noted
4. **Initialize QUALITY_SCORE.md**
   - List all domains
   - Set initial grades (typically C — unverified)
   - Define grading criteria
5. **Set up `docs/` directory structure** (per `templates/repo-scaffold.md`)
   - `docs/design-docs/`
   - `docs/product-specs/`
   - `docs/runbooks/`
   - `docs/adr/` (architecture decision records)
6. **Copy baseline compliance policies** to `helios/policies/general/`
   - Standard security policies
   - Data handling policies
   - Logging and audit policies
7. **Gather and author client policies** in `helios/policies/client/` (if applicable)
   - Client-specific regulatory requirements
   - Industry-specific compliance rules
8. **Generate enforcement manifests from policies** (agent-assisted)
   - One manifest per policy domain
   - Each manifest references specific rules, checks, and scoped files
9. **Validate manifests against `manifest-schema.yml`**
   - Schema validation passes
   - All referenced files and checks exist

## Phase 1 Checklist

- [ ] ARCHITECTURE.md complete and reviewed by Architecture Guardian
- [ ] Core beliefs documented
- [ ] At least 1 MVP product spec written
- [ ] QUALITY_SCORE.md initialized
- [ ] `docs/` structure created
- [ ] Policies in `helios/policies/general/`
- [ ] Enforcement manifests generated and valid
- [ ] All docs committed and pushed

## Handoff to Phase 2

Phase 1 is complete when agents can read the repo and understand:
- **What** the project is
- **How** it's structured
- **What** the quality standards are
- **What** compliance rules apply

## Cross-References

- Architecture template: `templates/ARCHITECTURE.md.template`
- Repo scaffold: `templates/repo-scaffold.md`
- Manifest schema: `helios/manifest-schema.yml`
- Quality scoring: `QUALITY_SCORE.md`
