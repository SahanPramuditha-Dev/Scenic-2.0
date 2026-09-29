# Scenic 2.0 — Group execution plan

This document converts the product vision into a practical group-development workflow. It complements `PROJECT.md`, `PLAN.md`, `docs/BACKLOG.md` and `docs/GIT_WORKFLOW.md`.

## 1. Working principle

Build Scenic as a set of **small vertical slices** that can be demonstrated end-to-end. Avoid building the entire frontend, backend and AI service independently and attempting integration at the end.

Preferred order:

1. authentication + ownership;
2. catalogue search/details;
3. watchlist + movie completion;
4. series/episode tracking + Continue Watching;
5. dashboard/statistics;
6. deterministic recommendation baseline;
7. recommendation integration;
8. optional franchise/universe tracking;
9. stabilization, deployment and presentation.

## 2. Core workstreams

| Workstream | Main responsibility | Main branch |
|---|---|---|
| Frontend / UX | React pages, state handling, responsive UI, accessibility | `feature/frontend-foundation` |
| Backend / Data | Express API, auth, Prisma, PostgreSQL, provider adapters | `feature/backend-foundation` |
| Tracking Core | Watchlist, history, movie/episode progress, Continue Watching | `feature/tracking-core` |
| AI / Decision | FastAPI intelligence service, ranking, reason codes, evaluation | `feature/ai-service-foundation` |
| Franchise / Universe | Hierarchies, memberships, watch orders and derived progress | `feature/franchise-universe-tracking` |
| QA / Testing | Test plans, integration tests, release evidence | `test/qa-foundation` |
| CI / Delivery | GitHub Actions, build checks, deployment and release automation | `chore/ci-cd-foundation` |
| Documentation / Presentation | Docs, diagrams, meeting notes and presentation assets | `docs/project-presentation` |

These are **starting workstream branches**, not permanent personal branches. Feature work should become smaller issue-specific branches as development progresses.

## 3. Integration sequence

### Slice A — first complete movie flow
Sign in → search movie → open details → add to watchlist → mark watched → dashboard count changes.

This slice proves:
- auth works;
- provider metadata is mapped;
- frontend/API/database integration works;
- user ownership is enforced;
- statistics can be derived from persisted data.

### Slice B — series progress
Search/open series → mark episode watched → derive season/series progress → Continue Watching shows next episode.

### Slice C — recommendation baseline
Backend prepares candidate set → Python service ranks candidates → reason codes return → frontend displays recommendations → fallback works if AI service is unavailable.

### Slice D — franchise/universe tracking
Only after core tracking is stable: show one mixed-media universe with released-title progress, next unwatched item, watch-order switch and clear denominator rules.

## 4. Sprint checkpoints

### Sprint 0 — kickoff and contracts
- confirm team roster and assessment rubric;
- assign owner + reviewer per workstream;
- freeze MVP scope;
- select metadata provider;
- approve auth/session approach;
- approve initial Prisma model and API conventions;
- agree exact runtime versions;
- create initial GitHub issues.

**Exit:** every P0 task has an owner, reviewer and acceptance criteria.

### Sprint 1 — foundations
- scaffold web, API and decision service;
- configure PostgreSQL + Prisma migration;
- implement auth foundation;
- add health endpoints;
- add lint/typecheck/test commands;
- create CI checks.

**Exit:** a fresh clone can run all services and CI is green.

### Sprint 2 — first vertical slice
- search/details provider adapter;
- watchlist;
- movie completion/history;
- dashboard movie count;
- frontend loading/empty/error states.

**Exit:** first end-to-end flow demonstrated from a clean database.

### Sprint 3 — series tracking
- seasons/episodes;
- episode events;
- season/series progress;
- Continue Watching / Up Next;
- progress boundary tests.

### Sprint 4 — intelligence baseline
- candidate filtering;
- weighted ranking;
- reason codes;
- cold-start behavior;
- timeout/fallback behavior;
- frontend recommendation surface.

### Sprint 5 — optional P1 features
Only if P0 is stable:
- ratings;
- richer statistics;
- Entertainment DNA;
- franchise/universe tracking;
- custom lists.

### Sprint 6 — stabilization and delivery
- security review;
- accessibility checks;
- integration tests;
- deployment;
- demo data;
- presentation rehearsal;
- contribution evidence.

## 5. Handoff contract between workstreams

Before another workstream depends on your code, provide:
- documented input/output contract;
- example request/response;
- error behavior;
- sample or seeded data;
- one happy-path test;
- one important failure-path test.

Frontend should not guess backend response shapes. Backend should not guess AI response shapes. The AI service should not own application persistence.

## 6. Pull-request rule

Every PR should answer:
1. What user/system outcome changed?
2. Which issue does it close or advance?
3. How was it tested?
4. Did API/schema/environment variables change?
5. Are screenshots required?
6. What should the reviewer specifically verify?

Prefer PRs small enough to review in one focused session.

## 7. Shared-file conflict zones

Coordinate before changing:
- `schema.prisma`;
- auth/session middleware;
- shared API types;
- root package scripts;
- environment variable names;
- design tokens/global CSS;
- CI workflow files;
- collection/universe membership rules.

## 8. Weekly evidence

Keep links to:
- issues completed;
- PRs merged;
- reviews performed;
- tests added;
- screenshots/demo recordings;
- important decisions.

Do not reconstruct contribution evidence at the end of the project.

## 9. Immediate next actions

1. Fill real team members into `docs/TEAM.md`.
2. Convert P0 backlog items into GitHub issues.
3. Select exact Node.js, Python and PostgreSQL versions.
4. Select metadata provider and document attribution/quota rules.
5. Approve auth/session design.
6. Agree first Prisma schema draft.
7. Scaffold the three services.
8. Complete Slice A before adding optional features.
