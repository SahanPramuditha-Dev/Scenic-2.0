# Setup and onboarding

## Current state
This repository contains planning documentation only. There is no working install, development server, database migration or CI command yet.

## Scaffolding checklist
1. Confirm runtime versions as a team; choose maintained compatible Node.js and Python versions and record them.
2. Create apps/web using React + TypeScript.
3. Create apps/api using Express + TypeScript; add Prisma and PostgreSQL integration.
4. Create services/decision using FastAPI and a reproducible Python dependency file.
5. Add package/dependency lockfiles and documented format, lint, typecheck, test and dev scripts.
6. Add .env.example with placeholders. Keep real .env files ignored.
7. Add a development PostgreSQL service or document a local database installation.
8. Add an initial migration and synthetic seed data.
9. Add API and decision-service health endpoints.
10. Configure CI only after the actual scripts and runtime versions are established.

## Planned environment inventory
| Component | Variable | Meaning |
|---|---|---|
| API | DATABASE_URL | PostgreSQL connection secret |
| API | SESSION_SECRET | Only if the chosen session implementation needs it |
| API | METADATA_API_KEY | Provider credential, if required |
| API | METADATA_BASE_URL | Allowlisted provider endpoint |
| API | DECISION_SERVICE_URL | Private service address |
| API | DECISION_SERVICE_TOKEN | Service authentication secret if used |
| API | WEB_ORIGIN | Allowed frontend origin |
| Web | VITE_API_BASE_URL | Public API origin; never a secret |
| Decision | DECISION_SERVICE_TOKEN | Validate API caller if token auth is chosen |

Variable names are proposed. Update this table to match code at scaffolding.

## New teammate validation after implementation
Clone the repository, use documented runtimes, install locked dependencies, copy environment examples, start PostgreSQL, apply migrations, load synthetic fixtures and start services.
Then sign in, search, save, mark watched and verify the dashboard.
The scaffolding PR must replace this checklist with exact tested commands for Windows and the team's deployment environment.

## Troubleshooting to document
Port conflicts, missing environment values, database readiness, migrations, provider quota errors, CORS/session configuration and decision-service downtime.
