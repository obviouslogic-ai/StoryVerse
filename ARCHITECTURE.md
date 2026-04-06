# StoryVerse Architecture

## Current State: Static MVP

The MVP is a single-file static application (`index.html`) with no backend, no build step, and no runtime dependencies beyond CDN-loaded libraries. It must be served over HTTP (not opened as a local file) because it uses `fetch()` for data loading.

```
HTTP Server (npx serve . / Vercel / Netlify)
  └── index.html
        ├── Tailwind CSS (CDN)
        ├── Chart.js (CDN)
        ├── Google Fonts (CDN)
        └── data/sample-characters.json (fetched at startup, inline fallback)
```

### Pages (client-side routing via CSS class `.active` on `.page` divs)

| Route slug | Section | Description |
|------------|---------|-------------|
| `home` | Landing | Hero, features grid, reader & author pricing, footer |
| `library` | Library | Data-driven book cards from JSON, genre filters (static), "More Coming Soon" CTA |
| `chat` | Chat | Character sidebar (data-driven), message thread with canned responses, suggested prompts |
| `author-dashboard` | Dashboard | Upload (simulated), Characters (data-driven), Settings (UI only), Analytics (Chart.js) |

### Data Flow

On startup, `fetch('./data/sample-characters.json')` loads books and characters. If the fetch fails (e.g. opened as a file), inline `FALLBACK_CHARACTERS` and `FALLBACK_BOOKS` arrays provide identical data so the app still works.

All data-driven views (library grid, character sidebar, dashboard character list) render from the same `state.characters` and `state.books` arrays. Chat responses are selected randomly from per-character `responses` arrays. No LLM calls are made.

### State Model

A single `state` object tracks:

| Key | Type | Purpose |
|-----|------|---------|
| `characters` | Array | Active character data (from fetch or fallback) |
| `books` | Array | Active book data |
| `currentCharacterIndex` | Number | Selected chat character |
| `currentPage` | String | Active page slug |
| `dataSource` | String | `'fetch'` or `'fallback'` |
| `chartsInitialized` | Boolean | Prevents Chart.js double-init |
| `uploadRunning` | Boolean | Guards against duplicate upload simulations |

### Interaction Model

Every visible control falls into one of two categories:
- **Functional demo**: navigation, library cards, chat input, dashboard tabs, upload simulation, settings sliders/checkboxes, Test Chat links
- **Explicitly disabled**: Sign In, Get Started, subscription buttons, Edit Profile — all call `showComingSoon()` with a descriptive label

No control is silently dead.

## Planned Production Architecture

See `docs/TECHNICAL_SPECS.md` for the full production stack.

### High-Level Target

```
Vercel (Next.js SSR/SSG)
  ├── Auth (Clerk/Auth0)
  ├── Stripe (payments)
  └── API routes
        └── Backend (FastAPI / Fastify)
              ├── PostgreSQL (users, sessions)
              ├── Redis (cache)
              ├── Pinecone/Weaviate (vector search)
              └── LLM (Claude / GPT-4)
                    └── Manuscript ingestion pipeline
```

### Migration Path

1. Scaffold Next.js app, move markup into React components.
2. Add auth (Clerk) and payment (Stripe) integrations.
3. Build API layer for chat, manuscript upload, and analytics.
4. Integrate LLM for real character conversations with canon validation.
5. Replace hardcoded data with PostgreSQL + vector DB.
