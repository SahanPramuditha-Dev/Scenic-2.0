# Test strategy

No tests have been executed: application code does not yet exist.

| Area | Essential cases | Layer |
|---|---|---|
| Authentication | Valid/invalid login, logout invalidation, expired session | API integration |
| Ownership | User B attempts access/mutation of User A's records | API integration |
| Watchlist | Duplicate add, repeated delete, refresh persistence | Integration/E2E |
| Movies | Mark twice, unmark, invalid series ID | Unit/integration |
| Episodes | Specials, future air dates, unknown air dates, new aired episode | Unit/integration |
| Dashboard | Multi-genre overlap, empty history, exact counts | Unit/integration |
| Catalog | Missing image, provider timeout, malformed response, quota | Adapter integration |
| Recommendations | Cold start, exclusion, tie order, missing signals, empty pool | Python unit/contract |
| Service fallback | Timeout, invalid response, unknown returned ID | API integration |
| UI | Keyboard flow, narrow width, loading/empty/error | Manual/E2E |
| Delivery | Clean database, migration, health and rollback | Release rehearsal |

## Fixtures
Use two users and synthetic titles: one movie with two genres, another with missing runtime, and a series containing regular aired, future and special episodes.
Use fixed evaluation timestamps so progress tests remain deterministic.
Mock external providers in automated tests; use a separate bounded manual integration check.

## Release gates
- Core requirements R01–R10 have recorded evidence.
- Relevant automated checks pass on the release commit.
- No unresolved critical security or data-loss defects.
- Fresh setup and seed work from documented commands.
- Recommendation outage does not break tracking.
- Known limitations and remaining lower-priority defects are documented.

## Evidence template
Date; commit; environment; requirement IDs; command or manual steps; expected result; actual result; pass/fail; issue link.
Report measured performance with dataset and environment. Do not invent coverage or accuracy percentages.
