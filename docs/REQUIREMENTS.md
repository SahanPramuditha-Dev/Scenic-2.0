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
| R11 | P1 | Franchise/universe tracking | Versioned curated hierarchy supports universe/continuity/saga/phase/chapter/franchise groupings; personal progress is derived from movie/episode history; inclusion policy and denominator are visible |
| R12 | P1 | Ratings/feedback | Validate rating range; each user's rating is unique per title |
| R13 | P1 | Export | Export own data only; output documented and tested |
| R14 | P1 | Advanced tracking state | Support planning, watching, completed, paused/on-hold, dropped and rewatching without destroying watch history |
| R15 | P1 | Watch orders | A collection may expose release, chronological or curated orders; switching order changes next-item guidance but never rewrites watched history |
| R16 | P1 | Related-media graph | Titles can express sequel, prequel, spin-off, same-universe, reboot/alternate-continuity and similar relations without forcing all relationships into one hierarchy |

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
Franchise/universe progress defaults to released eligible content; unreleased announced titles are shown separately unless the user selects another policy.
Separate continuities (for example DCU, DCEU and Arrowverse) must remain independently trackable unless a curated parent collection explicitly combines them.
Any displayed franchise completion percentage must identify its policy (for example released required titles, eligible episodes or estimated runtime); never show an undefined mixed-media percentage.
A title may belong to multiple franchises/collections without duplicating the user's watch event.
