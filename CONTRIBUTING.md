# Contributing

## Work cycle
1. Select a backlog item; create a GitHub issue with acceptance criteria, owner and dependencies.
2. Branch from current main: feat/short-topic, fix/short-topic or docs/short-topic.
3. Keep the change focused. Include schema/API/documentation updates with behavior changes.
4. Run the relevant checks defined by the implemented service.
5. Open a pull request using the template. Link the issue and include evidence.
6. Another team member reviews behavior, ownership checks and tests.
7. Resolve feedback, merge, and update the backlog.

Main should remain demonstrable. Recommended repository rules are one peer approval and passing required checks once CI exists; these rules have not been configured automatically.

## Definition of ready
Clear user outcome; acceptance criteria; owner and reviewer; known dependencies; agreed API/schema changes.

## Definition of done
- Acceptance criteria demonstrated.
- Relevant automated tests pass; manual UI checks recorded.
- Errors, loading and empty states handled.
- Private resources enforce server-side ownership.
- No credentials or personal data committed.
- Documentation and migrations updated.
- Peer review completed and integration verified.

## Conventions
Use TypeScript in web/API and typed Python boundaries. Prefer existing project formatting once configured. Validate input at API boundaries. Keep business logic out of UI components and route handlers. Avoid unrelated rewrites.

Never commit .env files, access tokens, database dumps with personal data, generated dependencies or copied third-party media without permission. Use synthetic fixtures.

## Collaboration evidence
Link issues, PRs, reviews and test evidence in meeting notes. Record pair programming honestly. Do not assign work to unnamed people or fabricate contributions.
