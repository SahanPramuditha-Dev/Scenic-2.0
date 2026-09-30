# Project charter — Scenic 2.0

## Product statement

Scenic 2.0 is a movie, TV-series and anime tracking + entertainment-intelligence platform.

Its long-term model is:

**Memory → Taste → Decision**

Scenic remembers viewing activity, turns those signals into an understandable taste profile, and helps the user make the next viewing decision. Scenic does **not** host or stream video.

## Problem

Viewers often keep fragmented watchlists, forget where they stopped in a series, lose track of completed seasons, and still spend too long deciding what to watch. Existing lists also tend to behave like static poster walls instead of using personal history and context.

## Primary users

Individual viewers who watch movies, TV series and/or anime and want one place to:
- discover titles;
- track viewing progress;
- organize watchlists and lists;
- understand viewing patterns;
- receive explainable recommendations;
- decide what fits their current time, mood and commitment.

## Academic MVP objectives

1. A new user can register, sign in, search, save a title and mark it watched in one complete demonstration.
2. A series viewer can record episode progress and see correct season/series progress after refresh.
3. Dashboard statistics agree with known seeded viewing records.
4. A user receives a bounded recommendation list with understandable reasons.
5. User A cannot read or modify User B's private records.
6. Core tracking remains usable if the Python decision service is unavailable.
7. The project can be installed and demonstrated reproducibly by another team member.

## Full product direction

The broader Scenic vision includes:
- movies, TV and anime discovery;
- Library statuses such as Watching, Completed, Plan to Watch, Paused and Dropped;
- Continue Watching and Up Next;
- Watchlist and Smart Queue;
- ratings, favorites, private notes and custom lists;
- Entertainment DNA and taste evolution;
- statistics, heatmaps and Year in Review;
- first-class franchise/universe progress such as Marvel, DC, Star Wars and anime franchises, with separate continuities, sagas/phases/chapters, watch orders and released-vs-upcoming progress;
- upcoming releases, calendar, notifications and availability intelligence;
- explainable recommendations and Scenic Match;
- Ask Scenic conversational discovery;
- Smart Watch Planner using time, mood, company and commitment;
- saved Watch Modes such as Bedtime, Quick Break, Weekend, Family and With Friends;
- contextual Taste Profiles so personal, family and friend viewing does not corrupt one preference model;
- effective remaining-runtime awareness, so a long title with 35 minutes left can still fit a 40-minute session;
- explainable **Why now? / Why later?** decisions and dynamic Smart Queue lanes such as Now, Tonight, Weekend and Later;
- recommendation refinement without restarting (shorter, darker, newer, already started, surprise me, etc.);
- recommendation memory/history and post-watch micro-feedback for better future decisions;
- progress-aware spoiler protection and safe recaps;
- import/export and deduplication;
- optional small-group decision features.

These are staged. The MVP should not be delayed by implementing every future feature.

## Core release scope

Authentication; metadata search/details; personal library/watchlist; movie completion; episode progress; Continue Watching; dashboard; deterministic recommendation baseline; responsive accessible UI; reproducible setup; tests and delivery documentation.

Anime is part of the product scope. Initial metadata may come through the primary movie/TV provider; a dedicated anime provider adapter can be added later if required.

## After core acceptance

Ratings and recommendation feedback; custom lists; first-class franchise/universe tracking; multiple watch orders and related-media relations; richer tracking states/rewatches; richer statistics; Entertainment DNA; Year in Review; upcoming/calendar; Smart Queue; import/export; availability intelligence; richer AI experiences.

## Initially excluded

Video streaming/CDN functionality; piracy links; payments; unrestricted public social feed/chat; advanced collaborative ML without data/evaluation; native mobile clients; offline synchronization; claims of AI accuracy without measured evidence.

## Deliverables

Source code; requirements; architecture; schema; API contracts; UI/page map; test evidence; reproducible local demo; deployment when feasible; group contribution evidence; project presentation; decision log.

## Technical baseline

- Frontend: React + TypeScript
- Main API: Node.js + TypeScript + Express
- ORM/database: Prisma + PostgreSQL
- Decision/AI service: Python + FastAPI
- External metadata: provider adapters, initially TMDB-oriented
- Optional later anime metadata adapter: AniList or another evaluated provider

Confirm exact runtime versions and external providers before scaffolding.

## Change control

Core acceptance criteria take priority over optional features. Record scope/architecture changes in docs/DECISIONS.md with reason, impact and owner.

A feature is complete only when implemented, reviewed, tested, integrated and documented.

## Tracking architecture reference
The full franchise/universe and advanced tracking model is specified in `docs/FRANCHISE_UNIVERSE_TRACKING.md`. Provider collections are treated as metadata inputs; Scenic owns the versioned hierarchy, relations, watch-order policy and derived personal progress.

## Recommendation architecture reference
The full context-aware recommendation and decision model—including Session Context, Watch Modes, Taste Profiles, effective watch time, Smart Queue lanes, Why Now/Why Later explanations, refinement, temporary-vs-permanent feedback, recommendation memory, streaming-aware ranking, story dependencies and release-driven catch-up planning—is specified in `docs/CONTEXT_AWARE_RECOMMENDATIONS.md`.
