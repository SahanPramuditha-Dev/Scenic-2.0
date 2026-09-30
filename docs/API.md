# Proposed API contract

Draft API prefix: /api/v1. These routes are not implemented yet.
All personal endpoints derive user identity from the authenticated session.

| Method | Route | Purpose |
|---|---|---|
| POST | /auth/register | Create account; 201 |
| POST | /auth/login | Start session; 200 |
| POST | /auth/logout | End session; 204 |
| GET | /me | Current profile |
| GET | /titles?q=&type=&page= | Catalog search |
| GET | /titles/:id | Internal title details |
| GET | /titles/:id/seasons | Series seasons |
| GET | /seasons/:id/episodes | Season episodes |
| GET | /me/watchlist | Paginated personal watchlist |
| PUT | /me/watchlist/:titleId | Idempotent save; 204 |
| DELETE | /me/watchlist/:titleId | Idempotent removal; 204 |
| PUT | /me/movies/:titleId/watched | Mark movie watched; 204 |
| DELETE | /me/movies/:titleId/watched | Unmark movie; 204 |
| PUT | /me/episodes/:episodeId/watched | Mark episode; 204 |
| DELETE | /me/episodes/:episodeId/watched | Unmark episode; 204 |
| GET | /me/progress/:titleId | Eligible/watched counts and completion |
| GET | /me/dashboard | Defined aggregate statistics |
| GET | /me/recommendations?limit=10 | Ranked candidates with reasons |
| GET | /collections | Browse curated franchise/universe collections |
| GET | /collections/:id | Collection identity, policy and summary |
| GET | /collections/:id/tree | Nested saga/phase/chapter/franchise structure |
| GET | /collections/:id/orders | Available release/chronological/curated watch orders |
| GET | /collections/:id/orders/:orderId | Ordered trackable items |
| GET | /titles/:id/collections | Universe/franchise memberships for a title |
| GET | /titles/:id/relations | Sequel/prequel/spin-off/same-universe/etc. relationships |
| GET | /me/collections/:id/progress | Personal released-title/episode/runtime progress under stated policy |
| GET | /me/collections/:id/next | Next eligible item in selected watch order |
| PUT | /me/collections/:id/preferences | Select watch order/inclusion preferences without changing history |
| GET | /me/titles/:titleId/state | Personal planning/watching/completed/paused/dropped/rewatching state |
| PUT | /me/titles/:titleId/state | Update personal tracking state |

## Common rules
- List response: { "items": [], "page": 1, "pageSize": 20, "total": 0 }. Where provider totals are unavailable, use an explicitly documented hasNextPage contract instead.
- Validate integers and enums; default page size 20, maximum 50. Recommendation limit 1–10.
- Error shape: { "error": { "code": "VALIDATION_ERROR", "message": "Readable explanation", "requestId": "..." } }.
- Status codes: 400 invalid request, 401 missing/invalid authentication, 403 forbidden operation, 404 absent resource, 409 conflict, 429 rate limit, 503 dependency unavailable.
- Do not leak stack traces, provider credentials or other users' existence/data.
- Watched PUT may accept watchedAt; validate format and policy. Omitting it uses server time. Repeated PUT preserves the original completion timestamp unless explicitly changed.
- Single-item PUT/DELETE operations are idempotent. Implement bulk season marking later as a transaction with explicit episode eligibility.
- Provider search results must resolve to stable internal title IDs before personal mutations.
- Collection progress responses must include the collection version and denominator policy.
- Unreleased items should be returned separately from released-only progress by default.
- A watch-order preference changes navigation/next-item behavior only; it must not rewrite watch history.
- Collection membership, canon/continuity labels and title relations come from Scenic's normalized/curated graph, not blindly from a provider collection endpoint.

## Private decision contract
POST /recommend with schemaVersion, candidate title metadata, aggregate genre preferences, excluded IDs and limit.
Return schemaVersion, algorithmVersion and items containing titleId, score and reasonCodes.
Do not pass names, email addresses, session tokens or password hashes.
Define request/response schemas and contract tests before parallel implementation; publish an OpenAPI specification when scaffolding begins.

## Context-aware decision extensions

These are **P1/P2 proposed contracts**, not academic-MVP commitments. Final request/response schemas must be agreed before implementation.

| Method | Route | Purpose |
|---|---|---|
| GET | /me/watch-modes | List reusable decision contexts |
| POST | /me/watch-modes | Create a custom Watch Mode |
| PATCH | /me/watch-modes/:id | Update a Watch Mode |
| DELETE | /me/watch-modes/:id | Delete a custom Watch Mode |
| GET | /me/taste-profiles | List contextual taste profiles |
| POST | /me/taste-profiles | Create family/friends/custom profile |
| PATCH | /me/taste-profiles/:id | Correct/update contextual profile settings |
| POST | /me/decisions | Create a recommendation session from explicit context |
| POST | /me/decisions/:sessionId/refine | Rerank the existing session with changes such as shorter/darker/newer/something-new |
| POST | /me/decisions/:sessionId/feedback | Record temporary or long-term recommendation feedback with explicit semantics |
| GET | /me/decisions/history | Recall prior recommendation sessions/results |
| GET | /me/smart-queue | Return explainable Now/Tonight/Weekend/Later/Continue/Catch-Up lanes |
| POST | /me/collections/:id/catch-up-plan | Build a progress-aware plan toward a target release/date |

Decision requests should distinguish persistent preferences from `sessionContext`. When time is specified, ranking should use **effective remaining watch time** for in-progress content where progress/runtime data is reliable. Recommendation results should return machine-readable reason codes/score components so the UI can explain taste fit, context fit, runtime fit and deferral. See `CONTEXT_AWARE_RECOMMENDATIONS.md`.
