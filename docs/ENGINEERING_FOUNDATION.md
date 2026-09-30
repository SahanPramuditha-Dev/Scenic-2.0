# Scenic 2.0 — Engineering Foundation Before Development

> **Purpose:** Define the project initialization work that should be completed before feature development begins.
>
> Scenic should start from a stable engineering foundation so frontend, backend, AI, database, testing and CI work can evolve in parallel without each contributor inventing a separate structure.

---

## 1. Foundation goals

Before feature development begins, the repository should provide:

- one consistent monorepo structure;
- pinned runtime/tool versions;
- a centralized frontend UI/design system;
- a working React frontend scaffold;
- a working Express + TypeScript API scaffold;
- a working FastAPI intelligence-service scaffold;
- PostgreSQL + Prisma initialization;
- validated environment configuration;
- shared code-quality rules;
- repeatable tests;
- API conventions;
- provider abstraction;
- seed/demo data;
- CI checks;
- a documented branch/PR workflow.

The purpose is not to over-engineer Scenic. The purpose is to make the first complete vertical slice reliable and reproducible.

---

## 2. Recommended initial repository structure

```text
Scenic-2.0/
├── apps/
│   ├── web/                  # React + TypeScript
│   └── api/                  # Express + TypeScript
│
├── services/
│   └── intelligence/         # Python + FastAPI
│
├── packages/
│   ├── shared-types/
│   ├── validation/
│   └── config/
│
├── prisma/
│   ├── schema.prisma
│   ├── migrations/
│   └── seed/
│
├── data/
│   ├── franchises/
│   ├── watch-orders/
│   └── fixtures/
│
├── docs/
├── presentations/
├── scripts/
├── infra/
├── .github/
├── package.json
├── pnpm-workspace.yaml
├── .env.example
└── README.md
```

See `PROJECT_STRUCTURE.md` for the detailed folder architecture.

---

## 3. Pin runtime and tool versions

Every contributor should use the same supported runtime/tool versions.

Decide and record:

- Node.js
- pnpm
- TypeScript
- Python
- PostgreSQL
- Prisma
- React
- FastAPI

Recommended files:

```text
.node-version
.python-version
package.json -> packageManager
.env.example
```

Do not allow each contributor to independently choose major runtime versions.

---

## 4. Initialize the monorepo workspace

Use a single repository with workspace management.

Recommended:

```text
pnpm workspace
```

Root responsibilities:

- shared scripts;
- workspace package discovery;
- lint/typecheck/test/build orchestration;
- shared developer commands.

Typical root scripts should eventually include:

```text
pnpm dev
pnpm lint
pnpm typecheck
pnpm test
pnpm build
```

---

## 5. Frontend initialization

Scaffold:

- Vite
- React
- TypeScript
- application routing
- query/data-fetching setup
- shared layouts
- error boundaries where appropriate
- environment loading

The frontend should never connect directly to PostgreSQL or private internal services.

---

## 6. Centralized UI and design system

The UI foundation must be created **before multiple pages are implemented**.

Recommended structure:

```text
apps/web/src/
├── ui/
│   ├── primitives/
│   ├── feedback/
│   ├── overlays/
│   ├── navigation/
│   ├── layout/
│   ├── data-display/
│   ├── media/
│   ├── recommendation/
│   ├── franchise/
│   ├── charts/
│   └── index.ts
│
├── design-system/
│   ├── tokens/
│   │   ├── colors.ts
│   │   ├── spacing.ts
│   │   ├── typography.ts
│   │   ├── radius.ts
│   │   ├── shadows.ts
│   │   └── breakpoints.ts
│   └── theme/
│
├── layouts/
└── features/
```

### UI ownership rule

```text
ui/
= reusable visual building blocks

features/
= Scenic-specific business composition
```

Examples that belong in centralized UI:

- Button
- Input
- Badge
- Modal
- Tabs
- EmptyState
- Skeleton
- MediaCard
- MediaPoster
- ProgressRing
- RecommendationCard
- UniverseCard

Examples that remain feature-specific:

- MCUPhaseSelector
- BedtimeModeConfigurator
- EntertainmentDNACorrectionPanel

If a visual component is useful across unrelated features, move it into `ui/`.

---

## 7. Styling decision

Choose one styling approach before page implementation.

Recommended direction:

```text
Tailwind CSS
+
central design tokens
+
central React UI components
```

Do not mix unrelated styling systems across contributors without a deliberate reason.

---

## 8. Backend API initialization

Scaffold the main trusted application backend using:

- Node.js
- TypeScript
- Express

Core folders should include:

```text
apps/api/src/
├── config/
├── middleware/
├── modules/
├── providers/
├── integrations/
├── database/
├── jobs/
├── utils/
└── types/
```

Recommended domain modules:

- auth
- users
- catalog
- media
- tracking
- watchlist
- history
- progress
- ratings
- favorites
- lists
- statistics
- recommendations
- decisions
- watch-modes
- taste-profiles
- smart-queue
- franchises
- watch-orders
- catch-up
- calendar
- availability
- notifications
- import-export

The main backend remains the source of truth for user ownership, history, progress and authorization.

---

## 9. PostgreSQL + Prisma initialization

Initialize:

```text
prisma/
├── schema.prisma
├── migrations/
└── seed/
```

Initial schema should focus on the first vertical slice.

Suggested early entities:

```text
User
MediaTitle
Season
Episode

WatchlistEntry
ViewingEvent
EpisodeProgress
```

Later add:

```text
Rating
Favorite
List
RecommendationFeedback

Universe
Franchise
WatchOrder
MediaRelation

WatchMode
TasteProfile
RecommendationSession
```

Do not implement the entire future schema before the first usable flow exists.

---

## 10. Stable internal identifiers

External provider IDs must not become Scenic's primary database identity.

Prefer:

```text
MediaTitle
- id: Scenic UUID
- tmdbId: nullable unique
- anilistId: nullable unique
- imdbId: nullable
```

This keeps Scenic independent from one metadata provider.

---

## 11. Provider abstraction

Do not scatter direct provider requests throughout controllers or frontend pages.

Recommended:

```text
providers/
└── tmdb/
    ├── tmdb.client.ts
    ├── tmdb.mapper.ts
    ├── tmdb.types.ts
    └── tmdb.provider.ts
```

Application logic should consume a provider interface such as:

```text
catalogProvider.search(...)
catalogProvider.getDetails(...)
```

This makes future AniList or alternative provider support manageable.

---

## 12. Environment configuration

Each service should have an `.env.example` with variable names only.

Possible Node API variables:

```text
DATABASE_URL
TMDB_API_KEY
SESSION_SECRET
INTELLIGENCE_SERVICE_URL
INTELLIGENCE_SERVICE_SECRET
```

Possible Python variables:

```text
SCENIC_API_URL
SERVICE_SECRET
```

Validate configuration at process startup.

Recommended:

- Zod for Node/TypeScript
- Pydantic Settings for Python

Never commit real credentials.

---

## 13. Authentication architecture

Before implementing `feature/auth`, agree on:

- session or token strategy;
- login/logout lifecycle;
- frontend credential handling;
- protected-route behavior;
- backend authorization ownership;
- internal Node → Python service authentication;
- expiration/refresh policy if applicable.

Authentication should be intentionally designed rather than evolving separately in frontend and backend.

---

## 14. API conventions

Use a stable API prefix:

```text
/api/v1
```

Standardize error responses:

```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid media type",
    "requestId": "..."
  }
}
```

Standardize paginated responses:

```json
{
  "items": [],
  "page": 1,
  "pageSize": 20,
  "total": 100
}
```

Agree conventions before frontend/backend teams build independent contracts.

---

## 15. Intelligence service initialization

The Python service should be named around its broader responsibility:

```text
services/intelligence/
```

rather than treating the whole service as only the Decision Engine.

Initial endpoints can be simple:

```text
GET  /health
POST /recommendations
POST /decision
```

The first implementation can remain deterministic.

Do **not** require an LLM for the first working recommendation service.

Recommended flow:

```text
Node API
   |
   | validated JSON
   v
Python Intelligence
   |
   +-- filter
   +-- score
   +-- rank
   +-- reason codes
```

Later modules can add:

- context-aware ranking;
- Entertainment DNA;
- Smart Queue;
- semantic search;
- Ask Scenic support;
- recommendation memory;
- franchise intelligence;
- future ML.

---

## 16. Recommendation evaluation fixtures

Recommendation behavior should be testable from the beginning.

Create scenario fixtures such as:

```text
bedtime_40min.json
matrix_short_break.json
mcu_continue.json
movie_35_minutes_remaining.json
not_tonight_feedback.json
cold_start_user.json
```

These should verify that future ranking changes do not break expected behavior.

Example:

> A user with 40 minutes before bed should not receive a three-hour unwatched movie unless there is an explicit, explainable reason.

---

## 17. Testing foundations

Initialize test tooling before feature code grows.

### Frontend

- Vitest
- React Testing Library

### Node API

- Vitest or Jest
- Supertest

### Python Intelligence

- pytest

Suggested test categories:

- unit
- integration
- scenario/fixture
- end-to-end later

Tests should be added with features rather than postponed until submission week.

---

## 18. Logging and request tracing

Use a standard logger instead of scattered `console.log` calls.

Useful fields:

```text
timestamp
level
service
requestId
message
```

Never log:

- passwords;
- session tokens;
- API secrets;
- authorization headers;
- unnecessary personal data.

A request ID should flow through backend errors and logs where practical.

---

## 19. Seed and demo data

Create reproducible seed data early.

Useful initial fixtures:

- test user;
- Matrix titles;
- Loki/series/episode sample;
- MCU sample hierarchy;
- basic watch order;
- 40-minute recommendation case;
- partially watched long movie.

Seed data should support both development and demonstrations.

---

## 20. CI initialization

Each pull request should eventually verify:

### Web

```text
lint
typecheck
test
build
```

### API

```text
lint
typecheck
test
build
```

### Intelligence

```text
ruff
pytest
```

Do not configure fake CI steps that pass without running real project scripts.

---

## 21. Formatting and code quality

Recommended baseline:

### TypeScript

- ESLint
- Prettier

### Python

- Ruff
- pytest

Optional later:

- pre-commit
- lint-staged
- Husky

The goal is consistent code, not excessive tooling.

---

## 22. GitHub workflow

Recommended branch flow:

```text
feature/*
    |
    v
develop
    |
    v
main
```

Normal feature work should go through pull requests.

Recommended merge requirements:

- no unresolved conflicts;
- lint/typecheck/test pass;
- reviewer approval where practical;
- feature documentation updated when behavior/contracts change.

`main` should remain demonstrable and stable.

---

## 23. Useful repository governance files

Initialize or maintain:

```text
.github/
├── ISSUE_TEMPLATE/
│   ├── feature.yml
│   ├── bug.yml
│   └── task.yml
├── PULL_REQUEST_TEMPLATE.md
├── CODEOWNERS
└── workflows/
```

CODEOWNERS is useful when frontend/backend/AI responsibilities are split across the team.

---

## 24. Docker/dev environment

A lightweight Docker environment is useful for shared infrastructure.

Recommended initial use:

- PostgreSQL
- optional API/intelligence containers later

Do not make Docker mandatory for every contributor if native development is simpler.

Example:

```text
infra/
├── docker/
└── docker-compose.yml
```

---

## 25. First vertical slice

After foundation initialization, avoid building every Scenic page in parallel.

Build one complete end-to-end journey:

```text
Register/Login
      |
      v
Search movie
      |
      v
Open Movie Details
      |
      v
Add to Watchlist
      |
      v
Mark Watched
      |
      v
Persist in PostgreSQL
      |
      v
Dashboard count changes
```

This validates:

```text
React
  |
  v
Express
  |
  v
Prisma
  |
  v
PostgreSQL
```

Only after this works should the team expand aggressively into episodes, statistics, recommendation intelligence and universe tracking.

---

## 26. Things not required initially

Avoid premature complexity such as:

- Redis before there is a measured need;
- Kafka;
- Kubernetes;
- multiple databases;
- a vector database before semantic features require one;
- custom ML training pipelines;
- a microservice for every feature;
- native mobile clients;
- complex event-driven architecture.

The initial architecture is already sufficient:

```text
React
   |
   v
Express API
   |
   +---------> PostgreSQL + Prisma
   |
   +---------> Python Intelligence Service
```

---

## 27. Pre-development checklist

Before feature branches begin substantial implementation, confirm:

- [ ] runtime versions chosen and documented;
- [ ] monorepo/workspace initialized;
- [ ] React/Vite/TypeScript scaffold works;
- [ ] centralized UI/design-system structure exists;
- [ ] styling approach agreed;
- [ ] Express/TypeScript API boots;
- [ ] FastAPI intelligence service boots;
- [ ] PostgreSQL + Prisma initialized;
- [ ] initial migration works;
- [ ] `.env.example` files exist;
- [ ] env validation works;
- [ ] provider adapter interface exists;
- [ ] authentication approach is documented;
- [ ] API error/pagination conventions are agreed;
- [ ] test runners work locally;
- [ ] seed/fixture data exists;
- [ ] lint/format tooling works;
- [ ] CI runs real project checks;
- [ ] branch/PR workflow is understood;
- [ ] first vertical-slice issue is defined.

---

## 28. Recommended development order

```text
Engineering Foundation
        |
        v
Authentication
        |
        v
Catalog/Search
        |
        v
Watchlist + Movie Tracking
        |
        v
Episode Progress
        |
        v
Dashboard + Statistics
        |
        v
Recommendation Baseline
        |
        v
Context-Aware Recommendations
        |
        v
Universe/Franchise Experience
        |
        v
Entertainment DNA / Ask Scenic / Advanced Intelligence
```

---

## 29. Principle

> **Initialize only the foundations that reduce integration risk. Do not implement future complexity before the first complete user journey works.**

The goal of this phase is to make Scenic easy for multiple contributors to build consistently—not to finish the product architecture before development starts.
