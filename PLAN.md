# Delivery plan

Status: proposed. Week numbers are relative to the agreed kickoff date.

| Milestone | Timing | Outputs | Exit criteria |
|---|---|---|---|
| M0: Agree | Week 1 | Team roles, scope, wireframes, provider spike, contracts | Group approves MVP; representative movie and series metadata validated |
| M1: Foundation | Week 2 | Project scaffolds, database, authentication, CI | Clean setup works; protected API rejects unauthenticated access |
| M2: First complete flow | Week 3 | Search → details → watchlist → watched movie | UI/API/database flow works; ownership tests pass |
| M3: Series and statistics | Week 4 | Episode progress, seasons, dashboard | Known fixtures produce exact counts; progress persists |
| M4: Decision engine | Week 5 | Rules-based ranking, reasons, fallback | Deterministic recommendations; exclusions and outage behavior tested |
| M5: Integration | Week 6 | Responsive states, accessibility, optional collection | Core acceptance passes; optional scope added only with capacity |
| M6: Stabilize | Week 7 | Security checks, performance evidence, deployment | Release gates pass; backup/restore and rollback rehearsed |
| M7: Submit | Week 8 | Final demo, report, presentation, contribution evidence | Fresh-machine demo succeeds; team signs off |

## Immediate steps
1. Confirm deadline, team roster and assessment rubric.
2. Assign an owner and a reviewer to each workstream.
3. Select a metadata provider after checking episode coverage, attribution and quota requirements.
4. Agree on authentication and the database/API contracts before parallel implementation.
5. Sketch search, title details, watchlist, series progress and dashboard screens.
6. Scaffold apps/web, apps/api and services/decision; commit lockfiles and exact supported runtime choices.
7. Implement one vertical slice: sign in → find a movie → add to watchlist → mark watched.
8. Add regression tests for that slice before expanding series and recommendation behavior.

## Dependency order
Provider mapping and schema → catalog API → tracking → dashboard and recommendation inputs.
Authentication and ownership enforcement precede private tracking endpoints.
The web team may use agreed mock responses while API implementation proceeds.

## Scope checkpoints
End of Week 3: if the first flow is incomplete, defer collections and ratings.
End of Week 5: if recommendations slip, retain the deterministic baseline; defer ML.
End of Week 6: freeze new features and resolve defects.
If fewer weeks are available, reduce optional scope and retain testing/demonstration time.

## Weekly review
Review completed acceptance criteria, blockers, integration health and remaining effort. Update docs/BACKLOG.md and record decisions. Never describe unfinished features as completed in the report.
