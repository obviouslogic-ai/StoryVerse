# Deploy HELIos Rollback Runbook

## Purpose

Provide deterministic rollback when `Deploy HELIos` ends in `HOLD` or `BLOCK` after partial changes.

## Rollback Scope

- repo file staging rollback
- workflow and rules rollback
- platform object rollback (Linear/Notion/Supabase)
- integration unlink or disable fallback

## Inputs

- deployment `session_id`
- session artifacts from `docs/helios/deploy-sessions/<session_id>/`
- backup manifest generated during apply mode

## Rollback Levels

### Level 1: Repo-Only Rollback

Use when external provisioning did not execute.

1. revert staged HELIos files using backup manifest
2. restore prior `AGENTS.md` and workflow files
3. verify working tree clean and gates unchanged

### Level 2: Repo + Integration Rollback

Use when platform objects were not newly created but integrations changed.

1. complete Level 1
2. disable or revert integration settings changed in session
3. re-run verification checks for known-good baseline

### Level 3: Full Rollback

Use when new platform objects were created.

1. complete Level 2
2. remove bootstrap Linear project/issues created by session
3. archive/delete Notion pages/databases created by session
4. disable or delete Supabase project created by session (non-production only)
5. rotate any generated credentials if exposed

## Decision Rules

- If production data may be affected, require HAA sign-off before destructive steps.
- Never rollback by deleting resources with unknown ownership.
- Prefer disable/archive over delete when object provenance is uncertain.

## Post-Rollback Verification

- Confirm target repo no longer contains partially staged HELIos artifacts.
- Confirm integration state matches pre-deploy baseline.
- Confirm platform resources are consistent and documented.
- Publish rollback summary in session report.
