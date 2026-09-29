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
- franchise/universe progress such as Marvel;
- upcoming releases, calendar, notifications and availability intelligence;
- explainable recommendations and Scenic Match;
- Ask Scenic conversational discovery;
- Smart Watch Planner using time, mood, company and commitment;
- progress-aware spoiler protection and safe recaps;
- import/export and deduplication;
- optional small-group decision features.

These are staged. The MVP should not be delayed by implementing every future feature.

## Core release scope

Authentication; metadata search/details; personal library/watchlist; movie completion; episode progress; Continue Watching; dashboard; deterministic recommendation baseline; responsive accessible UI; reproducible setup; tests and delivery documentation.

Anime is part of the product scope. Initial metadata may come through the primary movie/TV provider; a dedicated anime provider adapter can be added later if required.

## After core acceptance

Ratings and recommendation feedback; custom lists; franchise progress; richer statistics; Entertainment DNA; Year in Review; upcoming/calendar; Smart Queue; import/export; availability intelligence; richer AI experiences.

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
