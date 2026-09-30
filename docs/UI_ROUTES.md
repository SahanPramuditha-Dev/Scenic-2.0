# Scenic 2.0 UI pages and routes

This is the shared page map for frontend, backend and AI integration planning. Exact route names may change, but ownership and product purpose should stay explicit.

## Public/authentication

| Route | Page | Purpose | Phase |
|---|---|---|---:|
| '/' | Landing | Product introduction when logged out | P1 |
| '/login' | Login | Authenticate | MVP |
| '/signup' | Sign up | Create account | MVP |
| '/onboarding' | Onboarding | Initial interests/preferences | P1 |

## Primary logged-in navigation

| Route | Page | Key content | Phase |
|---|---|---|---:|
| '/home' | Home | Continue Watching, Up Next, For You, watchlist picks, small stats, upcoming | MVP |
| '/discover' | Discover | Trending, genres, filters, personalized discovery | MVP |
| '/search' | Search | Universal title/person search and filters | MVP |
| '/library' | Library | Watching, Completed, Watchlist, Paused, Dropped, Favorites | MVP/P1 |
| '/watchlist' | Watchlist / Smart Queue | Saved titles; later ranked Now / Tonight / Weekend / Later / Continue / Catch-Up lanes | MVP/P1 |
| '/continue' | Continue Watching | In-progress series/anime and next episode | MVP |
| '/history' | History | Watched events and Quick Log | MVP |
| '/lists' | Lists | Custom collections | P1 |
| '/stats' | Statistics | Counts, genres, time, progress analytics | MVP/P1 |
| '/dna' | Entertainment DNA | Taste profile and explanations | P1 |
| '/wrapped' | Year in Review | Period summary | P1 |
| '/calendar' | Calendar / Upcoming | Releases and personal upcoming items | P1 |
| '/notifications' | Notifications | Release/reminder events | P2 |
| '/settings' | Settings | Account, privacy, region, spoiler, AI preferences | MVP/P1 |
| '/settings/watch-modes' | Watch Modes | Configure Bedtime, Break, Weekend, Family, Friends and custom session presets | P1 |
| '/settings/taste-profiles' | Taste Profiles | Manage personal/family/friends/custom contextual taste profiles | P1 |

## Discovery/detail routes

| Route pattern | Page | Notes |
|---|---|---|
| '/movies' | Movie discovery | Optional dedicated browse view |
| '/tv' | TV discovery | Optional dedicated browse view |
| '/anime' | Anime discovery | Dedicated experience when provider support is ready |
| '/title/:id' | Unified media detail | Recommended initial route |
| '/movie/:id' | Movie detail | Alternative typed route |
| '/series/:id' | Series detail | Seasons, episodes, progress |
| '/anime/:id' | Anime detail | Same tracking model with anime-aware metadata |
| '/person/:id' | Person detail | P2; actor/director filmography |

A detail page should support:
- metadata and provider attribution;
- franchise/universe memberships and related-media relations;
- watchlist status;
- watched/progress controls;
- rating/favorite controls when enabled;
- recommendation context;
- related titles;
- spoiler-safe behavior.

## Intelligence/decision routes

| Route | Page | Purpose | Phase |
|---|---|---|---:|
| '/decide' | Watch Next / Tonight | Short ranked choices using time, remaining runtime, Watch Mode, taste/context fit and Why Now/Why Later explanations | P1 |
| '/ask' | Ask Scenic | Conversational entertainment assistant | P2 |
| '/recommendations' | Recommendations | Personalized recommendation feed with reasons | MVP/P1 |
| '/recommendations/history' | Recommendation History | Recall prior suggestions, alternatives and accepted/deferred/dismissed results | P2 |
| '/planner' | Smart Watch Planner | Fit backlog to time/commitment/goals | P2 |
| '/franchises' | Universe / Franchise Hub | Browse Marvel, DC, Star Wars, anime and other trackable collections; in-progress/nearly-complete filters | P1 |
| '/franchises/:id' | Universe / Franchise detail | Hierarchy, released progress, upcoming count, selected watch order, next item, remaining commitment | P1 |
| '/franchises/:id/order/:orderId' | Watch Order | Release/chronological/curated sequence with per-item progress | P1 |
| '/franchises/:id/group/:groupId' | Saga / Phase / Chapter detail | Nested progress for a child grouping | P1 |
| '/availability' | Availability | Services/region intelligence | P2 |
| '/group' | Group decision | Small-circle shared picks | P2 |

## Required UI states

Every data-driven page should deliberately design:
- initial loading;
- partial/skeleton loading when useful;
- empty state;
- provider/network error;
- permission/session failure;
- unavailable artwork fallback;
- unavailable AI/decision service fallback;
- narrow mobile layout;
- keyboard focus state.

## Home page priority

Home is not a marketing page after login. Preferred order:
1. Continue Watching / Up Next.
2. A small 'Watch Next' decision card.
3. Personalized recommendations.
4. Watchlist/Smart Queue picks.
5. Current-week or compact statistics.
6. Trending-for-you / discovery.
7. Upcoming releases.

## Frontend/backend contract rule

Frontend teams may mock responses only from documented contracts. When a page depends on a new response shape, update docs/API.md or an agreed OpenAPI contract before independent implementations diverge.

## Context-aware decision UI rules

- Available time should support a tolerance rather than pretending runtime metadata is exact.
- Show remaining commitment for in-progress content where reliable.
- Recommendation cards should expose **Why now?** and, when deferred, **Why later?**.
- Recommendation refinement controls can update the current session without overwriting permanent taste.
- "Not tonight", "too long" and "wrong mood" are session feedback; "not interested" or "never recommend" may persist.
- Watch Mode and Taste Profile selection must be visible when they materially affect ranking.
- See `CONTEXT_AWARE_RECOMMENDATIONS.md`.

## AI boundary

Ask Scenic and Decision pages must not invent private user state. AI features receive explicit, server-authorized context from Scenic APIs. See AI_SYSTEM_HANDOFF.md.


## Franchise/universe UI rules

- Show released progress separately from announced/upcoming titles.
- State the completion policy/denominator next to every percentage.
- Keep separate continuities visually distinct.
- Support release, chronological and curated order without modifying watch history.
- For mixed movie/series/anime collections, show title, episode and estimated-runtime breakdowns.
- Surface "next unwatched item", "remaining runtime", optional/spin-off labels and child saga/phase/chapter progress.
- Universe pages consume backend-authoritative collection data; AI may explain or plan over it but must not invent canon/membership.

See `FRANCHISE_UNIVERSE_TRACKING.md`.
