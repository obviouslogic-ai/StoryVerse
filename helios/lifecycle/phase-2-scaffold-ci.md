# Phase 2: Scaffold and CI (Days 5–7)

## Goal

Bootstrap the application, verify CI pipeline, and connect all automation.

## Duration

3 days

## Active Agents

| Agent | Role in Phase 2 |
|-------|-----------------|
| Coding Execution Agent (CEA) | Bootstrap application |
| Architecture Guardian (AGA) | Verify scaffold matches ARCHITECTURE.md |
| Test Architect (ATADA) | Verify CI pipeline and initial test setup |
| Security Agent (STMA) | Verify auth and security configuration |
| Quality Metrics Agent (QMSA) | Establish baseline quality metrics |
| Release Readiness Agent (RRA) | Verify all gates are operational |

## Steps

1. **Bootstrap application framework** (Next.js, SvelteKit, etc.)
   - Initialize project with recommended starter
   - Configure TypeScript, ESLint, Prettier
   - Verify directory structure matches ARCHITECTURE.md
2. **Configure Supabase connection** (if applicable)
   - Database schema initialization
   - Row-level security policies
   - Environment variable wiring
3. **Set up authentication flow** (if applicable)
   - Auth provider configuration
   - Session management
   - Protected route middleware
4. **Write initial tests** (minimum coverage)
   - At least 1 unit test (utility function or component)
   - At least 1 integration test (API route or data flow)
   - Verify test runner configuration
5. **Verify CI pipeline**: all jobs pass on a test PR
   - Lint job passes
   - Type-check job passes
   - Test job passes
   - Build job passes
   - Structural check job passes
   - Reliability gate passes (idempotency/retry/reconciliation checks)
6. **Verify compliance gate** catches violations
   - Create deliberately bad PR (hardcoded secret, missing encryption, etc.)
   - Confirm compliance gate blocks merge
   - Clean up test PR
7. **Verify Codex review** triggers on PR
   - Open test PR
   - Confirm Codex review comment appears
   - Verify review quality and relevance
8. **Set up Notion changelog automation**
   - Verify fires on merge to main
   - Confirm changelog entry format is correct
9. **Set up Linear auto-linking**
   - Verify branch naming convention creates links
   - Confirm PR ↔ issue bidirectional links
10. **Run first quality score assessment**
    - Update QUALITY_SCORE.md with actual grades
    - Establish baseline metrics

## Phase 2 Checklist

- [ ] Application boots locally
- [ ] Auth working (if applicable)
- [ ] Database connected (if applicable)
- [ ] CI pipeline passes: lint, types, tests, build, structural checks
- [ ] Reliability gate passes for automation-enabled domains
- [ ] Compliance gate catches test violations
- [ ] Codex review triggers on PRs
- [ ] Notion changelog fires on merge
- [ ] Linear issues link to PRs
- [ ] Baseline quality metrics established
- [ ] First feature work can begin

## Handoff to Phase 3

Phase 2 is complete when the application boots, CI passes, and all automation is connected. Phase 3 is the ongoing development loop.

## Cross-References

- CI workflow: `.github/workflows/`
- Development loop: `lifecycle/development-loop.md`
- Architecture spec: `ARCHITECTURE.md`
- Quality scoring: `QUALITY_SCORE.md`
- Reliability standards: `reference/reliability/`
