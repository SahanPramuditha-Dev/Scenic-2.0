# Contributing to Scenic 2.0

## Branch model

Scenic uses a simple group-project workflow:

- 'main' is stable and demonstrable.
- 'develop' is the integration branch.
- Work branches start from the latest 'develop'.
- Feature/fix/docs/test branches return to 'develop' through pull requests.
- Release PRs move tested work from 'develop' to 'main'.

Do not use a personal long-lived branch as a replacement for pull requests.

## Work cycle

1. Select or create a GitHub issue with user outcome, acceptance criteria, owner and dependencies.
2. Pull the latest 'develop'.
3. Create a focused branch:
   - 'feature/short-topic'
   - 'fix/short-topic'
   - 'docs/short-topic'
   - 'test/short-topic'
   - 'refactor/short-topic'
4. Implement the smallest coherent change.
5. Update tests, API/schema docs and migrations when behavior changes.
6. Run relevant local checks.
7. Open a pull request to 'develop' using the repository template.
8. Another member reviews the change.
9. Resolve feedback and merge only after acceptance criteria pass.
10. Regularly integrate 'develop' and keep it demoable.
11. Create a release PR from 'develop' to 'main' at a milestone/release point.

See docs/GIT_WORKFLOW.md for details.

## Definition of ready

A task is ready when it has:
- a clear user/system outcome;
- acceptance criteria;
- an owner and reviewer;
- known dependencies;
- agreed API/schema impact;
- a realistic scope for one branch/PR.

## Definition of done

- Acceptance criteria demonstrated.
- Relevant automated tests pass.
- Manual UI states checked where applicable.
- Loading, empty and error states handled.
- Private resources enforce server-side ownership.
- No credentials or personal data committed.
- API, schema, migrations and docs updated.
- Peer review completed.
- Integrated behavior works on 'develop'.

## Engineering conventions

Use TypeScript for the web/API and typed Python models at service boundaries. Keep business logic out of React components and Express route handlers. Validate untrusted input at API boundaries. Use migrations for database changes. Use synthetic fixtures for tests/demo data.

Never commit .env files, access tokens, production database dumps, generated dependency folders or copied third-party media without permission.

## Commit style

Prefer small commits with clear intent, for example:
- 'feat: add episode progress endpoint'
- 'fix: prevent duplicate watched events'
- 'docs: document Smart Queue inputs'
- 'test: add cross-user authorization coverage'

## Collaboration evidence

Link issues, PRs, reviews and test evidence in meeting notes. Record pair programming honestly. Do not fabricate contributions or assign work to unnamed people.
