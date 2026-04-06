# StoryVerse Technical Specifications

## Current Demo Stack

### Frontend
- **Framework**: Vanilla HTML/CSS/JavaScript
- **Styling**: Tailwind CSS (CDN)
- **Charts**: Chart.js
- **Architecture**: Single-page application with client-side routing

### Features
- Responsive design (mobile-first)
- No build process required
- Fully static - deployable anywhere
- CDN dependencies only

## Production Architecture (Planned)

### Frontend Stack
- **Framework**: Next.js + React + TypeScript
- **Styling**: Tailwind CSS
- **State Management**: Zustand or React Context
- **Authentication**: Clerk or Auth0
- **Payments**: Stripe SDK

### Backend Stack
- **API**: Python FastAPI or Node.js (Fastify)
- **Database**: PostgreSQL (user data, sessions)
- **Cache**: Redis
- **Vector DB**: Pinecone or Weaviate
- **Knowledge Graph**: Neo4j

### AI/ML Pipeline
- **LLM**: Anthropic Claude or OpenAI GPT-4
- **Embeddings**: OpenAI text-embedding-3-large
- **NLP**: spaCy, Hugging Face Transformers
- **Orchestration**: LangChain/LangGraph

### Infrastructure
- **Hosting**: Vercel (frontend) + AWS/GCP (backend)
- **Storage**: AWS S3 or Cloudflare R2
- **CDN**: Cloudflare
- **Monitoring**: Sentry, DataDog
- **CI/CD**: GitHub Actions

## Data Models

### Character Profile
```json
{
  "id": "char_1",
  "name": "Aria Vance",
  "book_id": "book_1",
  "personality": {
    "traits": ["brave", "curious", "emotionally intelligent"],
    "big_five": {}
  },
  "voice": {
    "style": "poetic yet direct",
    "vocabulary_level": "advanced",
    "quirks": ["astronomical metaphors"]
  },
  "knowledge_boundaries": {
    "knows": ["astrophysics", "star lore"],
    "limited": ["pre-collapse Earth history"]
  },
  "emotional_state": {},
  "relationships": {}
}
```

### Book/World
```json
{
  "id": "book_1",
  "title": "The Last Starkeeper",
  "author": "Elena Morrison",
  "genre": ["Fantasy", "Sci-Fi"],
  "characters": ["char_1", "char_2"],
  "settings": [],
  "narrative_structure": {},
  "themes": []
}
```

## API Endpoints (Planned)

### User Endpoints
- `POST /api/auth/login`
- `POST /api/auth/register`
- `GET /api/user/profile`
- `GET /api/user/subscriptions`

### Chat Endpoints
- `POST /api/chat/message`
- `GET /api/chat/history/:sessionId`
- `POST /api/chat/scenario` (what-if)

### Author Endpoints
- `POST /api/author/manuscript/upload`
- `GET /api/author/characters`
- `PUT /api/author/character/:id`
- `GET /api/author/analytics`

### Library Endpoints
- `GET /api/library/books`
- `GET /api/library/book/:id`
- `GET /api/library/characters`
