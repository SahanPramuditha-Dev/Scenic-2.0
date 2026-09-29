# Team onboarding

Use this checklist for every Scenic 2.0 group member before implementation starts.

## Read first

1. `README.md`
2. `PROJECT.md`
3. `PLAN.md`
4. `docs/PRODUCT_VISION.md`
5. `docs/FEATURE_MATRIX.md`
6. `docs/ARCHITECTURE.md`
7. `docs/GROUP_EXECUTION_PLAN.md`
8. `docs/GIT_WORKFLOW.md`
9. the document for your workstream.

## Git setup

Clone and start from the integration branch:

```bash
git clone https://github.com/SahanPramuditha-Dev/Scenic-2.0.git
cd Scenic-2.0
git checkout develop
git pull origin develop
```

Create focused work from `develop`:

```bash
git checkout -b feature/short-topic
```

Do not use a member-name branch as the normal workflow.

## Before writing code

Confirm with the team:
- your assigned issue;
- acceptance criteria;
- reviewer;
- dependencies;
- API/schema impact;
- whether another member is editing the same shared file.

## Local tools to standardize

The team should record exact versions after scaffolding:
- Node.js;
- npm/pnpm/yarn chosen by the team;
- Python;
- PostgreSQL;
- Git;
- optional Docker version if used.

Commit lockfiles. Do not allow each member to use incompatible major versions without documenting support.

## Secrets

Never commit:
- `.env`;
- database passwords;
- provider API keys;
- JWT/session secrets;
- service tokens;
- production data.

Use `.env.example` with placeholders only.

## Definition of a valid teammate setup

A new member should eventually be able to:
1. clone the repo;
2. install locked dependencies;
3. start PostgreSQL;
4. apply migrations;
5. load synthetic seed data;
6. start web/API/decision services;
7. sign in;
8. search a title;
9. add it to the watchlist;
10. run tests.

If this cannot be done from the written docs, setup documentation is incomplete.

## Communication

For blockers, report:
- what you expected;
- what actually happened;
- exact error/log;
- branch/commit;
- what you already tried.

Avoid silent API/schema changes. Record important design changes in `docs/DECISIONS.md`.

## Before opening a PR

- update from `develop`;
- run relevant lint/typecheck/tests;
- remove debug code;
- verify no secrets were added;
- update docs when contracts changed;
- add screenshots for UI changes;
- write clear verification steps.
