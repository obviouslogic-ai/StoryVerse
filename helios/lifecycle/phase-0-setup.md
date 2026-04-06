# Phase 0: Project Setup (Days 1–2)

## Goal

From nothing to a configured, connected project ready for knowledge base creation.

## Duration

2 days

## Active Agents

| Agent | Role in Phase 0 |
|-------|-----------------|
| Human Approval Authority (HAA) | Makes initial platform and architectural decisions |
| Project Manager (PPMA) | Guides setup sequence |

## Steps

1. **Create all platform accounts** (see `setup/01-accounts-and-access.md`)
   - GitHub organization / repository access
   - Vercel project
   - Supabase project (if applicable)
   - Linear workspace and team
   - Notion workspace
   - OpenAI / Codex access
2. **Create GitHub repository**
   - Initialize with README.md
   - Set default branch to `main`
3. **Copy `helios/` folder into project root**
   - Verify all subdirectories: `policies/`, `lifecycle/`, `setup/`, `templates/`
4. **Install Cursor rules** (`.cursor/rules/`)
   - Copy all rule files from helios templates
   - Verify rules load in Cursor
5. **Install GitHub workflows** (`.github/workflows/`)
   - CI pipeline workflow
   - Compliance gate workflow
   - Codex review workflow
   - Changelog automation workflow
6. **Customize and place AGENTS.md**
   - Fill in project-specific agent configurations
   - Define escalation paths
   - Set approval thresholds
7. **Store all secrets** (see `setup/02-secrets-and-api-keys.md`)
   - GitHub Secrets for CI
   - `.env.local` for local development
   - Vercel environment variables for deployment
8. **Configure MCP servers** (see `setup/03-mcp-configuration.md`)
   - Verify each MCP connection
   - Test round-trip communication
9. **Wire integrations** (see `setup/04-integrations.md`)
   - Linear ↔ GitHub (branch auto-linking)
   - Notion ↔ GitHub (changelog automation)
   - Vercel ↔ GitHub (deploy on merge)
10. **Configure branch protection on `main`**
    - Require PR reviews
    - Require CI to pass
    - No direct pushes

## Phase 0 Checklist

- [ ] All platform accounts created
- [ ] Repository exists with `helios/`, `.cursor/rules/`, `.github/workflows/`
- [ ] AGENTS.md customized and committed
- [ ] All secrets stored in GitHub Secrets, `.env.local`, Vercel
- [ ] MCP servers configured and verified
- [ ] Integrations connected and verified
- [ ] Branch protection active on `main`

## Handoff to Phase 1

Phase 0 is complete when **all items above are checked**. Phase 1 begins immediately.

## Cross-References

- Account setup details: `setup/01-accounts-and-access.md`
- Secrets reference: `setup/02-secrets-and-api-keys.md`
- MCP configuration: `setup/03-mcp-configuration.md`
- Integration wiring: `setup/04-integrations.md`
