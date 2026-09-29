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

## Common rules
- List response: { "items": [], "page": 1, "pageSize": 20, "total": 0 }. Where provider totals are unavailable, use an explicitly documented hasNextPage contract instead.
- Validate integers and enums; default page size 20, maximum 50. Recommendation limit 1–10.
- Error shape: { "error": { "code": "VALIDATION_ERROR", "message": "Readable explanation", "requestId": "..." } }.
- Status codes: 400 invalid request, 401 missing/invalid authentication, 403 forbidden operation, 404 absent resource, 409 conflict, 429 rate limit, 503 dependency unavailable.
- Do not leak stack traces, provider credentials or other users' existence/data.
- Watched PUT may accept watchedAt; validate format and policy. Omitting it uses server time. Repeated PUT preserves the original completion timestamp unless explicitly changed.
- Single-item PUT/DELETE operations are idempotent. Implement bulk season marking later as a transaction with explicit episode eligibility.
- Provider search results must resolve to stable internal title IDs before personal mutations.

## Private decision contract
POST /recommend with schemaVersion, candidate title metadata, aggregate genre preferences, excluded IDs and limit.
Return schemaVersion, algorithmVersion and items containing titleId, score and reasonCodes.
Do not pass names, email addresses, session tokens or password hashes.
Define request/response schemas and contract tests before parallel implementation; publish an OpenAPI specification when scaffolding begins.
