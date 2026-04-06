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
| Routing | Client-side JS (`navigateTo()`, CSS class `.active` on `.page` divs) |
| Data | `fetch('./data/sample-characters.json')` with inline JS fallback |
| Build | None required |
| Hosting | Any static HTTP server (Vercel, Netlify, GitHub Pages, `npx serve .`) |

## How to Run Locally

This app uses `fetch()` to load data, so it **must be served over HTTP** rather than opened as a file:

```bash
npx serve .
# or
npm run dev
```

## Coding Conventions

1. All application code lives in `index.html`. Do not split into separate JS/CSS files without explicit approval.
2. Use only CDN-loaded dependencies (Tailwind, Chart.js, Google Fonts). No npm runtime dependencies.
3. Tailwind dynamic class names (e.g. `bg-${color}-600`) do not work with the CDN; use an explicit map of full class strings instead (see `AVATAR_BG` in script).
4. No `console.log` in committed code except for error paths.
5. Escape user-provided text before inserting into the DOM. The MVP uses `textContent` for user chat messages and `escapeHtml()` for character data rendered via `innerHTML`. Production must never use `innerHTML` with unsanitized input.
6. File size limit: keep `index.html` under 2000 lines. If it grows beyond that, discuss splitting strategy before acting.
7. Every visible button must either perform a demo action or call `showComingSoon()` with a descriptive label. No dead/silent controls.
8. All buttons must have explicit `type="button"` to prevent implicit form submission.

## Demo vs. Production Status

| Feature | Status | Notes |
|---------|--------|-------|
| Landing page (hero, features, pricing) | Demo complete | Static markup, no backend |
| Library browse | Demo complete | Data-driven from `sample-characters.json` with fallback |
| Character chat | Demo complete | Canned responses from inline array, no LLM |
| Author dashboard — upload | Demo complete | Simulated progress bar with completion state, no file I/O |
| Author dashboard — characters | Demo complete | Data-driven profiles with Test Chat link |
| Author dashboard — settings | Demo complete | UI only, "Save" shows toast, not persisted |
| Author dashboard — analytics | Demo complete | Chart.js with hardcoded data |
| Mobile navigation | Demo complete | Hamburger menu for narrow viewports |
| Authentication | Not implemented | Buttons show "coming soon" toast |
| Payments / subscriptions | Not implemented | Pricing CTAs show "coming soon" toast |
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
2. Serve the site over HTTP (`npx serve .`) and verify all four pages work.
3. Check browser console for errors during the primary demo journey.
4. Verify no enforcement manifest violations in scoped domains.
5. Iterate until clean.
6. Then open PR.

## Where to Look

| Task | Document |
|------|----------|
| Add a new feature | `docs/MVP_FEATURES.md` |
| Understand architecture | `ARCHITECTURE.md` |
| Deployment options | `docs/DEPLOYMENT_GUIDE.md` |
| Technical roadmap | `docs/TECHNICAL_SPECS.md` |
| Compliance policies | `helios/policies/enforcement/manifests/` |
