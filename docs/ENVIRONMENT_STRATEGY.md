# Environment and data strategy

Scenic should behave consistently across local development, automated tests and the final demo.

## Environments

| Environment | Purpose | Data |
|---|---|---|
| Local development | individual coding and manual checks | synthetic/local only |
| Automated test | deterministic unit/integration tests | isolated fixtures |
| Shared integration/demo | team integration and rehearsal | synthetic demo accounts |
| Production-like deployment | final hosted demonstration if required | synthetic or approved test data |

Do not use real private viewing data as a project requirement.

## Service boundaries

Suggested local services:
- web: React + TypeScript;
- API: Express + TypeScript;
- database: PostgreSQL;
- decision service: FastAPI;
- optional provider/mock service for deterministic testing.

Exact ports should be committed to setup documentation once scaffolding exists. Avoid hard-coding localhost URLs inside application logic.

## Environment variables

Keep server secrets server-side. The browser may only receive variables intentionally safe to expose.

Planned categories:
- database connection;
- auth/session secret;
- metadata provider key/base URL;
- decision-service URL/token;
- allowed web origin;
- public web API base URL.

Maintain a root or service-level `.env.example` after scaffolding.

## Database rules

1. Prisma schema is the authoritative database model.
2. Every schema change requires a migration.
3. Do not manually edit another teammate's database as the only setup step.
4. Seed scripts must be repeatable and use synthetic data.
5. Tests should not depend on the developer's normal local database.
6. Destructive migrations require explicit review.

## Demo data

Prepare deterministic demo accounts covering:
- new/cold-start user;
- movie-heavy viewer;
- series/anime progress;
- watchlist backlog;
- completed and in-progress items;
- optional franchise/universe progress;
- recommendation feedback when implemented.

Never place real passwords or secrets in documentation.

## External provider strategy

The API owns provider access. The frontend should not need provider credentials.

For tests:
- use recorded/synthetic provider fixtures where legally appropriate;
- test timeout, missing fields, quota/error responses;
- do not make all CI tests depend on a live provider.

## Decision service outage behavior

Core tracking must remain available if the Python service is unavailable. Recommendation endpoints should return a controlled fallback/error rather than breaking unrelated Scenic pages.

## Version pinning

Once implementation begins, record exact supported runtime versions in `docs/SETUP.md` and CI. Keep dependency lockfiles committed.
