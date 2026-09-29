# Initial backlog

All items are unstarted. Convert these rows to GitHub issues during kickoff; assign real owners then.

| ID | Priority | Task | Depends on | Completion evidence |
|---|---|---|---|---|
| B01 | P0 | Confirm roster, rubric, deadline and scope | — | Approved meeting note |
| B02 | P0 | Evaluate metadata provider and attribution | B01 | Movie/series/episode sample and quota notes |
| B03 | P0 | Wireframe core screens | B01 | Reviewed flows including empty/error states |
| B04 | P0 | Approve schema and API/auth design | B02 | Contract and architecture decision |
| B05 | P0 | Scaffold web/API/decision and development DB | B04 | Fresh setup demonstration |
| B06 | P0 | Configure real lint/typecheck/test CI | B05 | Passing PR checks |
| B07 | P0 | Implement authentication and authorization | B05 | Session and cross-user tests |
| B08 | P0 | Implement provider adapter and catalog | B02, B05 | Search/details tests with provider failure fixtures |
| B09 | P0 | Build watchlist and movie tracking | B07, B08 | First complete vertical flow |
| B10 | P0 | Build series episode progress | B09 | Aired/special/missing-data boundary tests |
| B11 | P0 | Build dashboard aggregates | B09, B10 | Exact fixture counts |
| B12 | P0 | Implement baseline Python ranking | B04, B08 | Deterministic fixture evaluation |
| B13 | P0 | Integrate recommendations and fallback | B09, B12 | Timeout and cold-start demonstration |
| B14 | P0 | Complete accessibility/responsive checks | B03, B09, B10, B11, B13 | Recorded keyboard/mobile checks |
| B15 | P0 | Complete security and integration testing | B06–B14 | Test report with no unresolved critical defects |
| B16 | P0 | Deploy or package reproducible demo | B15 | Health, migration and rollback evidence |
| B17 | P0 | Final report and presentation | B16 | Rehearsal and contribution record |
| B18 | P1 | Build franchise/universe tracking domain | B10, B11 | Versioned hierarchy, memberships, released-only progress and at least one mixed-media demonstration collection |
| B19 | P1 | Ratings and recommendation feedback | B13 | Validated per-user feedback |
| B20 | P1 | Export own tracking data | B15 | Ownership and format tests |
| B21 | P1 | Add advanced tracking states and rewatch-ready model | B09, B10 | Planning/watching/completed/paused/dropped/rewatching states preserve history |
| B22 | P1 | Add watch orders and related-media graph | B18 | Release/chronological order switch works; sequel/prequel/spin-off/continuity relations tested |
| B23 | P1 | Build Universe Hub/detail/progress UI | B03, B18, B22 | Hierarchy, next item, upcoming count, denominator policy and mixed-media breakdown visible |
| B24 | P1 | Integrate franchise progress with recommendations/Ask Scenic | B13, B18 | AI consumes backend-authoritative progress and never invents collection membership |

## Status updates
Maintain status, issue link and owner here or replace this table with links to the authoritative GitHub board. Do not maintain conflicting status copies.
