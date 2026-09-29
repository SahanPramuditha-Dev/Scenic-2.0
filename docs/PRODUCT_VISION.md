# Scenic 2.0 product vision

## Positioning

Scenic is a **Personal Entertainment Operating System** rather than a streaming clone.

It should answer three questions:

1. **What have I watched and where did I stop?**
2. **What does my history say about my taste?**
3. **What should I watch next, given my situation now?**

The guiding model is:

**Memory → Taste → Decision**

## Memory

Scenic should maintain a reliable record of:
- movies completed;
- series/anime progress by season and episode;
- Continue Watching and Up Next;
- watchlist/Plan to Watch;
- paused and dropped titles;
- favorites;
- ratings and recommendation feedback;
- rewatches;
- custom lists;
- franchise/universe hierarchy and progress;
- release/chronological/curated watch orders;
- sequel/prequel/spin-off/same-universe relations;
- viewing history and timestamps;
- optional private notes;
- stable provider/canonical IDs for import/export.

The Memory layer must remain useful even if recommendation services fail.

## Taste

Scenic derives understandable taste information from user-controlled data.

Examples:
- genre affinity by movie/TV/anime;
- preferred runtime/commitment;
- actor/director/studio patterns;
- franchise, universe, saga/phase/chapter and continuity completion;
- rating patterns;
- comfort genres versus exploration;
- taste evolution over time;
- negative preferences;
- Entertainment DNA;
- 'Why Scenic thinks this' explanations.

Taste must be editable/correctable. A temporary 'not tonight' signal must not automatically mean dislike.

## Decision

The product differentiator is helping users choose rather than showing another endless catalogue.

Decision features include:
- Watch Next / Decision Engine;
- Smart Queue;
- Scenic Match;
- explainable recommendations;
- Hidden Gems;
- Comfort-Zone Breaker;
- context-aware choices using time, mood, company and commitment;
- continue-versus-new decision;
- release/availability urgency;
- Smart Watch Planner;
- Ask Scenic conversational discovery;
- group/shared decision support as optional later scope;
- catch-up planning for a universe/franchise before a new release.

A good decision response is short, ranked and explainable rather than an infinite wall of posters.

## Product experience

Scenic should feel dark, cinematic, premium and content-first without cloning Netflix. Avoid excessive neon, fake complexity and decorative dashboards that do not help a viewing decision.

The logged-in Home page should behave like a personal command center, prioritizing:
- Continue Watching;
- Up Next;
- a small set of recommendations;
- useful watchlist picks;
- current viewing statistics;
- upcoming/relevant releases.

## Trust and safety principles

- Do not host or link pirated streams.
- Keep personal viewing data private by default.
- Enforce ownership server-side.
- Respect spoiler boundaries based on recorded progress.
- Make recommendation reasons inspectable.
- Allow taste correction and recommendation feedback.
- Keep export/import possible so user data is portable.
- Do not claim recommendation accuracy without evaluation.

## Delivery philosophy

Build Scenic in layers:

1. Foundation and identity.
2. Reliable tracking and history.
3. Library/watchlist and dashboard.
4. Franchise/universe tracking foundation using the same canonical history, with at least one curated demonstration collection after core tracking is stable.
5. Deterministic recommendation baseline.
6. Entertainment DNA and richer statistics.
7. Smart Queue and contextual decision intelligence.
8. Spoiler/availability intelligence.
9. Conversational and group features.
10. Advanced ML only when data and evaluation justify it.

The academic submission should prioritize a smaller system that is correct, demonstrable and testable over a large incomplete feature set.

## Franchise/universe tracking principle
Scenic must not equate a provider movie collection with a complete entertainment universe. The authoritative model is Scenic's own versioned hierarchy + relationship graph, documented in `FRANCHISE_UNIVERSE_TRACKING.md`. Separate continuities remain separate, upcoming items are not silently counted against released-only completion, and mixed-media percentages always state their denominator.
