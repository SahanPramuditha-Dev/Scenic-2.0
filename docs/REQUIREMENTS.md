# Requirements and acceptance criteria

Priority: P0 core; P1 after core. IDs are stable references for issues and tests.

| ID | Priority | Requirement | Acceptance |
|---|---|---|---|
| R01 | P0 | Authentication | Register/sign in/sign out; invalid credentials rejected; private endpoints reject unauthenticated access |
| R02 | P0 | Catalog search | Search movies/series with pagination; loading, empty, error and quota states visible |
| R03 | P0 | Title details | Title, type, genres, overview and available episode data shown; missing artwork has fallback |
| R04 | P0 | Watchlist | Add/remove own titles; repeating add does not duplicate entries; survives refresh |
| R05 | P0 | Movie history | Mark/unmark watched; repeated mark does not inflate statistics |
| R06 | P0 | Series progress | Mark/unmark episodes; season/series progress derived from eligible episodes |
| R07 | P0 | Dashboard | Distinct movies, completed series/seasons and genre counts agree with fixture data |
| R08 | P0 | Recommendations | Exclude ineligible/already-completed titles; return reasons; cold-start and unavailable states work |
| R09 | P0 | Ownership | A second user cannot access or change another user's watchlist or progress |
| R10 | P0 | Usability | Keyboard operable core flow; labeled inputs; visible focus; usable at narrow and desktop widths |
| R11 | P1 | Collections | Ordered collection entries and progress; order and inclusion policy displayed |
| R12 | P1 | Ratings/feedback | Validate rating range; each user's rating is unique per title |
| R13 | P1 | Export | Export own data only; output documented and tested |

## Proposed quality targets
Confirm these after measuring a representative dataset and environment.
- Internal read endpoints: p95 below 500 ms on a documented local test, excluding external-provider latency.
- Recommendation request: bounded timeout of 2 seconds at the API boundary, with a usable fallback.
- Catalog listing: maximum page size 50.
- No secrets in source, client bundles, fixtures or application logs.
- Every private resource has positive and cross-user authorization tests.

## Important product rules
Watchlist membership and viewing history are independent: completing a title does not silently delete its saved status.
Unwatching changes derived statistics immediately.
A multi-genre title contributes to each relevant genre count, so genre totals can exceed unique title totals.
Series completion is relative to a stated eligible episode set, and may change when newly aired episodes are imported.
