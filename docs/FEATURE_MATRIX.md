# Scenic 2.0 feature matrix

This file preserves the full agreed product catalogue while separating the academic MVP from later phases.

Legend:
- **MVP** — should be implemented for the first assessed working release.
- **P1** — add after MVP acceptance if capacity permits.
- **P2** — strategic/future expansion.

| Area | Feature | Phase | Notes |
|---|---|---:|---|
| Identity | Register, sign in, sign out | MVP | Private data scoped to authenticated user |
| Identity | Profile and preferences | P1 | Theme, region, spoiler and recommendation preferences |
| Discovery | Universal search | MVP | Movies, TV and anime-oriented results |
| Discovery | Discover/trending browsing | MVP | Provider-backed catalogue |
| Discovery | Movies / TV / Anime filters | P1 | Dedicated experiences can be added incrementally |
| Details | Media detail page | MVP | Overview, genres, artwork, type, seasons/episodes when available |
| Library | Watchlist / Plan to Watch | MVP | Unique per user/title |
| Library | Watching / Completed | MVP | Movie and episode/series state |
| Library | Paused / Dropped | P1 | Explicit status rather than inferred dislike |
| Library | Favorites | P1 | Independent from ratings/watchlist |
| Tracking | Movie completion | MVP | Idempotent |
| Tracking | Season/episode progress | MVP | Derive progress from eligible episodes |
| Tracking | Continue Watching / Up Next | MVP | Progress-aware |
| Tracking | Rewatch tracking | P1 | Separate repeated viewing events |
| History | Viewing history / Quick Log | MVP | User-owned activity |
| Ratings | 1–10 ratings | P1 | Unique per user/title |
| Notes | Private title notes | P2 | Not public social reviews by default |
| Lists | Custom lists | P1 | Ordered/curated user lists |
| Queue | Smart Watchlist / Smart Queue | P1 | Priority, age, commitment, availability/release pressure |
| Statistics | Movie/series/season/episode counts | MVP | Exact fixture-based calculations |
| Statistics | Genre distribution | MVP | Multi-genre titles may count in multiple categories |
| Statistics | Watch time / heatmaps | P1 | Requires reliable runtime/event data |
| Statistics | Completion/drop/rewatch analytics | P1 | Explicit definitions |
| Statistics | Year in Review / Wrapped | P1 | Derived from historical records |
| Taste | Entertainment DNA | P1 | Explainable profile, not a black box score |
| Taste | Taste evolution | P2 | Compare periods over time |
| Collections | Universe / continuity hierarchy | P1 | Generic universe → saga/era/chapter → phase/arc/franchise → title model; no Marvel/DC-specific tables |
| Collections | Franchise/universe progress | P1 | Released eligible title progress derived from canonical user history |
| Collections | Mixed-media progress breakdown | P1 | Show title, episode and estimated-runtime progress rather than an unexplained single percentage |
| Collections | Release vs chronological vs curated order | P1 | Switching order changes next-item guidance, never watch history |
| Collections | Optional/main-story inclusion | P1 | Main canon/required vs optional/spin-off policy must be visible |
| Collections | Separate continuities | P1 | DCU/DCEU/Arrowverse-style roots remain independent unless intentionally grouped |
| Collections | Related-media graph | P1 | Prequel, sequel, spin-off, same universe, reboot, alternate continuity, etc. |
| Collections | Universe Hub / detail | P1 | Browse, progress, hierarchy, next item, remaining runtime, upcoming items |
| Collections | Universe catch-up goals | P2 | Plan completion before an upcoming movie/season using remaining runtime and release date |
| Collections | Story dependency classification | P2 | Curated Required / Helpful / Optional prerequisites; AI must not invent canon dependencies |
| People | Actor/director/studio completion | P2 | Depends on metadata depth |
| Recommendations | Deterministic ranking baseline | MVP | Eligible candidate filtering + weighted scoring |
| Recommendations | Explainable reasons | MVP | Human-readable reason codes |
| Recommendations | Scenic Match | P1 | Personalized compatibility score with explanation |
| Recommendations | Hidden Gems | P1 | Discovery outside obvious popularity |
| Recommendations | Comfort-Zone Breaker | P2 | Controlled exploration |
| Recommendations | Feedback learning | P1 | Like/dislike/not tonight/never recommend; preserve temporary vs permanent intent |
| Recommendations | Why Now / Why Later explanations | P1 | Explain both strong current fits and high-taste titles deferred because of session context |
| Recommendations | Post-watch micro-feedback | P1 | Lightweight signals such as loved/good/okay/disliked plus optional strengths/weaknesses |
| Recommendations | Recommendation memory/history | P2 | Recall prior suggestions, alternatives and accepted/deferred/dismissed outcomes |
| Recommendations | Recommendation Sandbox / refinement | P2 | Rerank within the same session: shorter, darker, newer, more like this, something new, etc. |
| Decision | Watch Next / Decision Engine | P1 | Short ranked result set |
| Decision | Time/mood/company/commitment context | P1 | Context affects session, not permanent taste by default |
| Decision | Saved Watch Modes | P1 | Reusable Bedtime, Quick Break, Weekend, Family, Friends and custom contexts |
| Decision | Contextual Taste Profiles | P1 | Separate personal/family/friends taste signals without fragmenting the account |
| Decision | Effective remaining-runtime awareness | P1 | Rank by remaining commitment for in-progress movies/episodes, not only full title runtime |
| Decision | Smart Queue lanes | P1 | Dynamic Now / Tonight / Weekend / Later / Continue / Catch-Up organization |
| Decision | Exploration control | P2 | User-controlled Familiar ↔ Surprise Me behavior |
| Decision | Smart Watch Planner | P2 | Plans around available time and backlog |
| AI | Ask Scenic | P2 | Conversational layer over real Scenic data |
| AI | Entertainment Memory queries | P2 | Questions over personal history/progress |
| AI | Semantic/fuzzy discovery | P2 | Alias and intent-aware search |
| Spoilers | Progress-aware spoiler boundaries | P1 | Never reveal beyond tracked progress |
| Spoilers | Safe recap | P2 | Generated/retrieved within spoiler boundary |
| Calendar | Upcoming releases | P1 | Provider-backed |
| Calendar | Personal viewing/release calendar | P1 | Relevant upcoming items |
| Notifications | Release/episode reminders | P2 | Opt-in |
| Availability | Streaming availability | P2 | Region/provider data required |
| Availability | Subscription coverage intelligence | P2 | Helps prioritize accessible titles |
| Import/export | Export personal Scenic data | P1 | Document schema |
| Import/export | Import/deduplicate external history | P2 | Canonical IDs important |
| Social | Friends/small-circle activity | P2 | Privacy-first |
| Social | Group decision/shared queue | P2 | Uses member constraints/preferences |
| Quality | Responsive accessible UI | MVP | Keyboard, focus and narrow/desktop layouts |
| Quality | Loading/empty/error/offline-ish states | MVP | Graceful provider/AI failure |
| Security | Cross-user authorization protection | MVP | Required on every private resource |

## MVP success boundary

The project can be considered a successful first release without P1/P2 features if authentication, discovery, tracking, progress, dashboard statistics, privacy and the deterministic recommendation baseline work correctly and can be demonstrated reproducibly.

## Feature addition rule

Before implementing a P1/P2 feature:
1. link it to a GitHub issue;
2. define acceptance criteria;
3. identify data/API dependencies;
4. confirm it will not delay unresolved MVP defects.
