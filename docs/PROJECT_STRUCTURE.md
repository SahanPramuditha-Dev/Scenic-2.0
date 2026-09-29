# Planned project structure

Scenic 2.0 should begin as a single repository so the group can version frontend, API, decision service and shared documentation together.

    Scenic-2.0/
    ├─ apps/
    │  ├─ web/                  # React + TypeScript UI
    │  └─ api/                  # Express + TypeScript main API
    ├─ services/
    │  └─ decision/             # FastAPI Python decision/AI service
    ├─ packages/
    │  ├─ shared-types/         # Shared TypeScript contracts where useful
    │  └─ config/               # Shared lint/format config if adopted
    ├─ prisma/
    │  ├─ schema.prisma
    │  └─ migrations/
    ├─ docs/
    ├─ presentations/
    ├─ scripts/
    ├─ .github/
    │  ├─ ISSUE_TEMPLATE/
    │  └─ workflows/            # CI later
    ├─ README.md
    ├─ PROJECT.md
    ├─ PLAN.md
    └─ CONTRIBUTING.md

## apps/web

Owns presentation and interaction:
- routing;
- layouts/navigation;
- search/discovery UI;
- tracking controls;
- dashboards/charts;
- accessibility and responsive behavior.

It must not contain database credentials or call PostgreSQL directly.

## apps/api

Owns trusted application behavior:
- authentication/session validation;
- authorization/ownership;
- provider adapters;
- catalog normalization;
- library/watchlist/history;
- progress calculations;
- statistics queries;
- calls to the decision service;
- response contracts.

## services/decision

Owns recommendation/decision computation:
- candidate filtering/ranking;
- explanation reason codes;
- Scenic Match/Smart Queue algorithms as they evolve;
- evaluation scripts;
- future ML/semantic/LLM integrations.

It should not become the source of truth for user ownership or core watch history.

## prisma

Owns relational schema and migrations. Schema changes require review because they affect every workstream.

## shared boundaries

Prefer explicit HTTP/OpenAPI or versioned JSON contracts between Node and Python. Do not share a database as an undocumented communication mechanism between services.

## First scaffold sequence

1. Create package/workspace root.
2. Scaffold web.
3. Scaffold API.
4. Scaffold FastAPI decision service.
5. Add PostgreSQL/Prisma.
6. Add environment examples.
7. Add lint/test/build scripts.
8. Add CI after local scripts are stable.
9. Implement one vertical flow before building many isolated screens.

## Configuration rule

Commit '.env.example' files with variable names only. Never commit real API keys, JWT/session secrets, database passwords or production connection strings.
