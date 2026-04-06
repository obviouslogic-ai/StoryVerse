# StoryVerse

## Purpose

StoryVerse is an interactive literary platform that transforms static books into living, interactive worlds. Readers chat with AI-powered characters; authors upload manuscripts and control how their characters behave. This repository contains the static MVP demo.

## Architecture

See `ARCHITECTURE.md` for the domain map. See `docs/TECHNICAL_SPECS.md` for the planned production architecture.

## Documentation

- Product specs: `docs/MVP_FEATURES.md`
- Technical specs: `docs/TECHNICAL_SPECS.md`
- Deployment guide: `docs/DEPLOYMENT_GUIDE.md`

## Current Stack (MVP Demo)

| Layer | Technology |
|-------|-----------|
| Markup | Single `index.html` (vanilla HTML5) |
| Styling | Tailwind CSS via CDN (`cdn.tailwindcss.com`) |
| Charts | Chart.js via CDN |
| Routing | Client-side JS (`navigateTo()`, DOM show/hide) |
| Data | Inline JS arrays + `data/sample-characters.json` |
| Build | None required |
| Hosting | Any static host (Vercel, Netlify, GitHub Pages) |

## Coding Conventions

1. All application code lives in `index.html`. Do not split into separate JS/CSS files without explicit approval.
2. Use only CDN-loaded dependencies (Tailwind, Chart.js, Google Fonts). No npm runtime dependencies.
3. Tailwind dynamic class names (e.g. `bg-${color}-600`) do not work with the CDN; use an explicit map of full class strings instead.
4. No `console.log` in committed code except for error paths.
5. Escape user-provided text before inserting into the DOM. The MVP uses `textContent` for user chat messages. Production must never use `innerHTML` with unsanitized input.
6. File size limit: keep `index.html` under 2000 lines. If it grows beyond that, discuss splitting strategy before acting.

## Demo vs. Production Status

| Feature | Status | Notes |
|---------|--------|-------|
| Landing page (hero, features, pricing) | Demo complete | Static markup, no backend |
| Library browse | Demo complete | Hardcoded book cards |
| Character chat | Demo complete | Canned responses, no LLM |
| Author dashboard — upload | Demo complete | Simulated progress bar, no file I/O |
| Author dashboard — characters | Demo complete | Static profiles |
| Author dashboard — settings | Demo complete | UI only, not persisted |
| Author dashboard — analytics | Demo complete | Chart.js with hardcoded data |
| Authentication | Not implemented | Buttons render but do nothing |
| Payments / subscriptions | Not implemented | Pricing UI only |
| Real AI/LLM integration | Not implemented | Planned: Anthropic Claude or OpenAI |
| Manuscript ingestion pipeline | Not implemented | Planned: NLP + vector DB |
| Canon validation | Not implemented | Conceptual only |

## PR Conventions

- Branch: `[linear-id]-short-description` (or `feature/short-description` if no Linear issue)
- Commit: `[LINEAR-ID] description of change` (or conventional-commit style)
- Link Linear issue in PR description when available.

## Compliance

Before working in these domains, read the applicable enforcement manifest in `helios/policies/enforcement/manifests/`:

| Domain | Manifest |
|--------|----------|
| Authentication / Authorization | `access-control.manifest.yml` |
| Data handling / PHI / PII | `data-protection.manifest.yml` |
| Encryption / Key management | `infrastructure-config.manifest.yml` |
| Logging / Monitoring | `security-operations.manifest.yml` |
| Development practices | `development-change.manifest.yml` |

**Violation handling:** Critical/High block merge. Medium requires review. Low warns. See `helios/policies/enforcement/violation-classifications.md`.

**Escalation:** If a rule cannot be satisfied, STOP and escalate to Security Agent or HAA. No silent workarounds.

## Self-Review Loop

Before opening any PR:

1. Review changes against this `AGENTS.md`.
2. Verify the site loads and all four pages work (`index.html` opened locally or via `npx serve .`).
3. Verify no enforcement manifest violations in scoped domains.
4. Iterate until clean.
5. Then open PR.

## Where to Look

| Task | Document |
|------|----------|
| Add a new feature | `docs/MVP_FEATURES.md` |
| Understand architecture | `ARCHITECTURE.md` |
| Deployment options | `docs/DEPLOYMENT_GUIDE.md` |
| Technical roadmap | `docs/TECHNICAL_SPECS.md` |
| Compliance policies | `helios/policies/enforcement/manifests/` |
