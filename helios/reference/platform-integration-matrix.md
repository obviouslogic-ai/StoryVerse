# Platform Integration Matrix

> Canonical reference for all cross-platform integrations, MCP server availability, API capabilities, and programmatic setup constraints across the 10-platform stack.

---

## 1. Cross-Platform Integration Matrix

Rows = source platform initiating the integration. Columns = target platform.

| | GitHub | Linear | Notion | Figma | Supabase | Vercel | Slack | Asana | Outlook/Teams | Read.ai |
|---|---|---|---|---|---|---|---|---|---|---|
| **GitHub** | — | Native | Native | Native | Native | Native | Native | Native | Native (Teams) | None |
| **Linear** | Native | — | Native (embed) | Native | None | Native (narrow) | Native | Import-only | None | Native (new) |
| **Notion** | Native (sync) | Partial | — | Native | None | None | Native | Native (sync) | Limited | Native |
| **Figma** | Native | Native | Native | — | Native (Make) | Indirect (v0) | Native | Native | Native (Teams) | None |
| **Supabase** | Native | None | None | Native (Make) | — | Native | Custom | None | None | None |
| **Vercel** | Native | Partial | None | Indirect | Native | — | Native | None | None | None |
| **Slack** | Native | Native | Native | Native | Custom | Native | — | Native | Limited | Native |
| **Asana** | Native | None | None | Native | None | None | Native | — | Native | Native |
| **Outlook/Teams** | Native (Teams) | None | Limited | None | None | None | Limited | Native | — | Native |
| **Read.ai** | None | None | Native | None | None | None | Native | Native | Native | — |

### Legend

| Status | Meaning |
|---|---|
| **Native** | First-party integration built by one or both platforms |
| **Native (sync)** | First-party synced database with bidirectional data flow |
| **Native (embed)** | First-party link preview / embed only — no database sync |
| **Native (narrow)** | First-party but limited scope (e.g., Vercel preview comments → Linear issues only) |
| **Native (new)** | First-party integration launched recently (Feb 2026) |
| **Native (Make)** | First-party via Figma Make sub-product only |
| **Partial** | Limited native support (link previews or AI Connector only) |
| **Custom** | No native integration — requires custom webhooks, Edge Functions, or middleware |
| **Indirect** | Achievable via intermediary (e.g., Figma MCP → v0 → Vercel deploy) |
| **Import-only** | One-time migration import, no live sync |
| **Limited** | Basic integration, significant gaps (e.g., only AI Connector beta) |
| **None** | No integration path — native, third-party, or custom |

---

## 2. MCP Server Inventory

| Platform | Official MCP | Endpoint | Auth | Status | Capability |
|---|---|---|---|---|---|
| GitHub | Yes | `https://api.githubcopilot.com/mcp/` | OAuth / PAT | GA | Read-write (51+ tools) |
| Linear | Yes | `https://mcp.linear.app/mcp` | OAuth 2.1 | GA | Read-write (21+ tools) |
| Notion | Yes | `https://mcp.notion.com/mcp` | OAuth 2.0 | GA (v2.0.0) | Read-write |
| Figma | Yes | Remote: `https://mcp.figma.com/mcp` / Desktop: `http://127.0.0.1:3845/mcp` | OAuth | Beta | Read + limited write |
| Supabase | Yes | `https://mcp.supabase.com/mcp` | OAuth | GA | Full read-write |
| Vercel | Yes | `https://mcp.vercel.com` | OAuth | Beta | **Read-only** |
| Slack | Yes | Official remote (hosted) | OAuth | GA (Feb 2026) | Read-write |
| Asana | Yes | `https://mcp.asana.com/v2/mcp` | OAuth 2.0 | GA (V2, Feb 2026) | Read-write (30+ tools) |
| Microsoft 365 | Yes | Agent 365 platform / community servers | OAuth | GA | Read-write (Graph API) |
| Read.ai | **No** | N/A | N/A | N/A | Zapier MCP only |

### MCP Setup Commands

```bash
# GitHub
claude mcp add github -- npx -y @anthropic-ai/mcp-remote https://api.githubcopilot.com/mcp/

# Linear
claude mcp add linear -- npx -y mcp-remote https://mcp.linear.app/mcp

# Notion
claude mcp add notion -- npx -y @notionhq/notion-mcp-server

# Figma (remote)
claude mcp add figma -- npx -y @anthropic-ai/mcp-remote https://mcp.figma.com/mcp

# Supabase
claude mcp add supabase -- npx -y @anthropic-ai/mcp-remote https://mcp.supabase.com/mcp

# Vercel
claude mcp add vercel -- npx -y @anthropic-ai/mcp-remote https://mcp.vercel.com

# Slack
claude mcp add slack -- npx -y @anthropic-ai/mcp-remote <slack-mcp-endpoint>

# Asana
claude mcp add asana -- npx -y @anthropic-ai/mcp-remote https://mcp.asana.com/v2/mcp
```

---

## 3. API & Programmatic Capabilities

### What CAN Be Created Programmatically

| Platform | Programmatic Creation Capabilities |
|---|---|
| **GitHub** | Repos, branches, branch protection, Actions workflows, issues, PRs, labels, milestones, teams, org settings |
| **Linear** | Teams, projects, issues, labels, cycles, milestones, workflows, integrations (via Settings) |
| **Notion** | Pages, databases, database rows, blocks, comments, integrations (via Connections) |
| **Figma** | Comments, webhooks, Dev Mode annotations, variables, Code Connect mappings |
| **Supabase** | Organizations, projects, databases, tables, migrations, Edge Functions, auth config, branches, secrets |
| **Vercel** | Projects, deployments, domains, environment variables, Edge Config, team settings |
| **Slack** | Channels, messages, Canvases, user groups, app installations (admin), bookmarks |
| **Asana** | Workspaces (via org), teams, projects, tasks, sections, custom fields, goals, portfolios |
| **Microsoft 365** | Teams, channels, calendar events, emails, SharePoint sites/pages |
| **Read.ai** | Webhook configurations, integration connections (via UI) |

### What CANNOT Be Created Programmatically (Key Constraints)

| Platform | Limitation | Impact on Standup SOPs |
|---|---|---|
| **Figma** | Cannot create new files via API (REST API is read-only for file creation) | Manual step required: create initial file in Figma UI, then all subsequent operations via API/MCP |
| **Notion** | Cannot create workspaces or teamspaces via API | Manual step required: workspace/teamspace creation in UI; pages and databases can be created via API |
| **Vercel** | MCP server is read-only (Public Beta) | Vercel CLI or REST API required for write operations; MCP useful for inspection/monitoring only |
| **Read.ai** | No public API or MCP server | All setup is manual via Read.ai web UI; webhook output is the only programmatic touchpoint |
| **Supabase** | Subscription plan is org-scoped (cannot mix paid/free in same org) | Org selection is a prerequisite decision before project creation |
| **Slack** | App installations require admin consent | Workspace admin must approve each integration app before agent can configure channels |
| **Linear** | Workspace creation requires manual UI step | Teams, projects, and all sub-resources can be created via API after workspace exists |

---

## 4. Integration Scope Levels

Each integration operates at a specific scope level. This determines whether it must be configured once (account/workspace) or per-project.

| Integration | Scope Level | Setup Frequency |
|---|---|---|
| GitHub ↔ Linear | Workspace | Once per GitHub org + Linear workspace pair |
| GitHub ↔ Vercel | Team + Project | Per Vercel project (auto-deploys per repo) |
| GitHub ↔ Supabase | Project | Per Supabase project linked to repo |
| GitHub ↔ Notion | Per database | Per Notion synced database connection |
| GitHub ↔ Slack | Workspace + Channel | Once per workspace, then per-channel subscriptions |
| GitHub ↔ Figma | Workspace + File | Once per workspace, then per-file/branch links |
| GitHub ↔ Asana | Workspace | Once per GitHub org + Asana workspace |
| GitHub ↔ Teams | Organization | Once per GitHub org + Teams tenant |
| Linear ↔ Slack | Workspace | Once per Linear workspace + Slack workspace |
| Linear ↔ Figma | Per-user + File | Per-user plugin install, then per-file links |
| Linear ↔ Notion | Per-user | Per-user Notion link preview connection |
| Notion ↔ Slack | Workspace | Once per Notion workspace + Slack workspace |
| Notion ↔ Asana | Per database | Per synced database connection |
| Figma ↔ Slack | Workspace | Once per Figma org + Slack workspace |
| Slack ↔ Asana | Workspace | Once per Asana workspace + Slack workspace |
| Asana ↔ Outlook | Per-user | Per-user calendar sync |
| Read.ai ↔ Slack | Per-user | Per-user Read.ai account connection |
| Read.ai ↔ Asana | Per-user | Per-user Read.ai account connection |
| Read.ai ↔ Notion | Per-user | Per-user Read.ai account connection |
| Read.ai ↔ Outlook | Per-user | Per-user calendar connection |

---

## 5. Integration Hub Rankings

Platforms ranked by native integration coverage across the 10-platform stack:

| Rank | Platform | Native Integrations | Coverage |
|---|---|---|---|
| 1 | **Slack** | 7/9 | GitHub, Linear, Notion, Figma, Vercel, Asana, Read.ai |
| 2 | **GitHub** | 7/9 | Linear, Notion, Figma, Supabase, Vercel, Slack, Asana + Teams |
| 3 | **Figma** | 6/9 | GitHub, Linear, Notion, Slack, Asana, Teams + Supabase (Make) |
| 4 | **Notion** | 5/9 | GitHub (sync), Figma, Slack, Asana (sync), Read.ai |
| 5 | **Asana** | 5/9 | GitHub, Figma, Slack, Outlook, Read.ai |
| 6 | **Linear** | 4/9 | GitHub, Figma, Slack, Read.ai + Notion (partial) + Vercel (narrow) |
| 7 | **Vercel** | 3/9 | GitHub, Supabase, Slack + Linear (partial) |
| 8 | **Read.ai** | 4/9 | Slack, Asana, Notion, Outlook/Teams |
| 9 | **Outlook/Teams** | 3/9 | GitHub (Teams), Asana, Read.ai |
| 10 | **Supabase** | 2/9 | GitHub, Vercel + Figma (Make) |

---

## 6. Optimal Standup Sequence

Based on dependency ordering, integration scope levels, and hub connectivity:

| Phase | Order | Platform | Rationale |
|---|---|---|---|
| **1 — Foundation** | 1 | GitHub | Foundation for all dev integrations; most platforms connect to it first |
| | 2 | Supabase | Backend infrastructure; org + project needed before Vercel can link |
| | 3 | Vercel | Deployment; connects to GitHub (auto-deploy) and Supabase (env vars) |
| **2 — Engineering** | 4 | Linear | Engineering execution; connects to GitHub, Slack, Figma, Notion |
| | 5 | Figma | Design system; connects to GitHub, Linear, Slack, Notion |
| **3 — Knowledge** | 6 | Notion | Knowledge management; connects to GitHub, Linear, Figma, Slack, Asana |
| | 7 | Slack | Communication hub; connects to 7 platforms — best done after targets exist |
| **4 — Business** | 8 | Asana | Business visibility; connects to GitHub, Figma, Slack, Notion, Outlook, Read.ai |
| | 9 | Outlook/Microsoft 365 | Calendar & email; connects to Asana, Read.ai, GitHub (Teams) |
| | 10 | Read.ai | Meeting intelligence; connects to Slack, Asana, Notion, Outlook |

---

## Related Documents

- SOPs: `../sops/platform-standup/` — Individual platform standup SOPs
- Setup: `../setup/04-integrations.md` — Existing integration guides (subset)
- MCP Config: `../setup/03-mcp-configuration.md` — MCP server configuration
- Secrets: `../setup/02-secrets-and-api-keys.md` — Secret inventory
