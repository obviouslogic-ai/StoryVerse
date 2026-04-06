# HELIos General Baseline Policies

This folder contains the SSC (baseline) policy set adapted for the HELIos pipeline. It serves as the default compliance baseline for all projects.

## Source
- **Origin:** SSC policy library (Dropbox)
- **Adapted:** Cross-references updated from `docs/policies/` to relative paths for use under `helios/policies/general/`

## Structure
- **10 policy domains:** access-control, data-protection, development-change, security-operations, infrastructure-configuration, business-continuity, governance-risk-compliance, endpoint-asset-management, workforce-training, third-party-contracts
- **Appendices:** system-evidence.md, document-library.md (project-specific customization)
- **Second-tier artifacts:** plans, registers, checklists, catalogs-and-schedules, logs-and-records, templates

## Usage
1. Copy this baseline into new projects as-is, or
2. Replace with your organization's policy set using the same structure
3. Generate enforcement manifests from the markdown policies (see `../README.md` and `../enforcement/`)

## Customization
- **appendices/system-evidence.md** — Replace SSC-specific paths with your project's codebase references
- **index.md References** — Add project-specific CAIQ or audit artifacts (e.g., `CAIQ_architecture_overview.md`, `CAIQ_completed.csv`) if applicable
