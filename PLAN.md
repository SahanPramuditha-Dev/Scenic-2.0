# Delivery plan

Status: proposed. Week numbers are relative to the agreed kickoff date.

| Milestone | Timing | Outputs | Exit criteria |
|---|---|---|---|
| M0: Agree | Week 1 | Team roles, scope, wireframes, provider spike, contracts | Group approves MVP; representative movie and series metadata validated |
| M1: Foundation | Week 2 | Project scaffolds, database, authentication, CI | Clean setup works; protected API rejects unauthenticated access |
| M2: First complete flow | Week 3 | Search → details → watchlist → watched movie | UI/API/database flow works; ownership tests pass |
| M3: Series and statistics | Week 4 | Episode progress, seasons, dashboard | Known fixtures produce exact counts; progress persists |
| M4: Decision engine | Week 5 | Rules-based ranking, reasons, fallback | Deterministic recommendations; exclusions and outage behavior tested |
| M5: Integration | Week 6 | Responsive states, accessibility, optional first-class franchise/universe tracking slice | Core acceptance passes; optional scope added only with capacity |
| M6: Stabilize | Week 7 | Security checks, performance evidence, deployment | Release gates pass; backup/restore and rollback rehearsed |
| M7: Submit | Week 8 | Final demo, report, presentation, contribution evidence | Fresh-machine demo succeeds; team signs off |

For workstream ownership, handoffs and sprint checkpoints, use [docs/GROUP_EXECUTION_PLAN.md](docs/GROUP_EXECUTION_PLAN.md).

## Immediate steps
1. Confirm deadline, team roster and assessment rubric.
2. Assign an owner and a reviewer to each workstream in [docs/TEAM.md](docs/TEAM.md).
3. Ensure every member completes [docs/TEAM_ONBOARDING.md](docs/TEAM_ONBOARDING.md).
4. Select a metadata provider after checking episode coverage, attribution and quota requirements.
5. Agree on authentication and the database/API contracts before parallel implementation.
6. Select exact Node.js, Python and PostgreSQL versions and update setup/environment docs.
7. Sketch search, title details, watchlist, series progress, dashboard and the P1 Universe/Franchise progress screen.
8. Scaffold `apps/web`, `apps/api` and `services/decision`; commit lockfiles and exact supported runtime choices.
9. Configure CI only after real lint/typecheck/test scripts exist.
10. Implement one vertical slice: sign in → find a movie → add to watchlist → mark watched → confirm dashboard change.
11. Add regression tests for that slice before expanding series and recommendation behavior.
12. Convert P0 rows from `docs/BACKLOG.md` into GitHub issues with owners/reviewers.
13. Review [docs/RISK_REGISTER.md](docs/RISK_REGISTER.md) at the weekly integration checkpoint.

## Dependency order
Provider mapping and schema → catalog API → tracking → dashboard and recommendation inputs.  
Authentication and ownership enforcement precede private tracking endpoints.  
The web team may use agreed mock responses while API implementation proceeds.

## Scope checkpoints
End of Week 3: if the first flow is incomplete, defer P1 franchise/universe UI and ratings, but keep the data model forward-compatible.  
End of Week 5: if recommendations slip, retain the deterministic baseline; defer ML.  
End of Week 6: freeze new features and resolve defects.  
If fewer weeks are available, reduce optional scope and retain testing/demonstration time.

## Weekly review
Review completed acceptance criteria, blockers, integration health, risk changes and remaining effort. Update `docs/BACKLOG.md`, contribution evidence and `docs/DECISIONS.md`.

## Release gate
Before merging `develop` to `main`, complete [docs/RELEASE_DEMO_CHECKLIST.md](docs/RELEASE_DEMO_CHECKLIST.md). Never describe unfinished features as completed in the report or presentation.
