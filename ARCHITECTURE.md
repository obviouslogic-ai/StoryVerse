# StoryVerse Architecture

## Current State: Static MVP

The MVP is a single-file static application (`index.html`) with no backend, no build step, and no runtime dependencies beyond CDN-loaded libraries.

```
Browser
  └── index.html
        ├── Tailwind CSS (CDN)
        ├── Chart.js (CDN)
        ├── Google Fonts (CDN)
        └── data/sample-characters.json (optional fetch)
```

### Pages (client-side routing via DOM show/hide)

| Route slug | Section | Description |
|------------|---------|-------------|
| `home` | Landing | Hero, features grid, reader & author pricing |
| `library` | Library | Book cards with genre filters (static) |
| `chat` | Chat | Character sidebar + message thread (canned responses) |
| `author-dashboard` | Dashboard | Upload, Characters, Settings, Analytics tabs |

### Data Flow

All data lives inline in `<script>` as the `characters` array. `data/sample-characters.json` mirrors this data for external consumption but is not loaded at runtime by default.

Chat responses are selected randomly from a per-character `responses` array. No LLM calls are made.

## Planned Production Architecture

See `docs/TECHNICAL_SPECS.md` for the full production stack (Next.js, FastAPI, PostgreSQL, vector DB, LLM integration).

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
