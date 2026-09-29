# Scenic 2.0 — Franchise, Universe & Advanced Tracking System

> **Purpose:** Define Scenic's first-class tracking model for movies, TV series, anime, franchises, cinematic universes, sagas, phases, chapters, timelines, watch orders, and related-media graphs.
>
> **Product principle:** Scenic is a tracking-first entertainment intelligence platform. AI may reason over tracking data, but the authoritative progress model belongs to the main Scenic backend.

---

## 1. Why this needs its own subsystem

A simple provider "collection" is not enough for Scenic.

Scenic needs to represent:

- movie franchises
- cinematic universes
- TV universes
- anime franchises
- sagas
- phases
- chapters
- timelines / continuities
- release orders
- chronological orders
- recommended orders
- spin-offs
- prequels / sequels
- alternate continuities
- reboots
- crossovers
- individual movie progress
- series / season / episode progress
- rewatches
- user status and history

Examples include:

- Marvel Cinematic Universe
- DC Universe (DCU)
- DC Extended Universe (DCEU)
- Arrowverse
- Star Wars
- Wizarding World
- Middle-earth
- Fast & Furious
- Mission: Impossible
- Pokémon
- Naruto
- Dragon Ball
- Gundam
- One Piece and other long-running anime/media franchises

The model must remain generic. **Do not hard-code Marvel-specific or DC-specific database structures.**

---

# 2. Research findings that affect the design

## 2.1 TMDB collections are useful, but too flat

TMDB exposes movie collection details with a collection and its `parts`. This is useful for straightforward movie-series grouping, but it does not by itself model all of the following Scenic needs:

- a hierarchy such as Universe -> Saga -> Phase
- multiple valid watch orders
- cross-media movie + television membership
- alternate continuities
- anime-style sequel / prequel / side-story graphs
- Scenic-specific inclusion policies

Therefore TMDB collection IDs should be treated as **provider metadata**, not as Scenic's complete franchise model.

Reference:
- https://developer.themoviedb.org/reference/collection-details

## 2.2 Anime relations are naturally graph-shaped

AniList models relationships such as:

- PREQUEL
- SEQUEL
- PARENT
- SIDE_STORY
- SPIN_OFF
- ALTERNATIVE
- COMPILATION
- CONTAINS
- SAME_UNIVERSE

This demonstrates why anime and some large franchises cannot be represented cleanly as one flat ordered list.

References:
- https://docs.anilist.co/reference/enum/mediarelation
- https://docs.anilist.co/guide/graphql/queries/media

## 2.3 Tracking status needs more than watched / unwatched

Modern tracking systems commonly distinguish states such as:

- planning / plan to watch
- currently watching
- completed
- paused / on hold
- dropped
- rewatching

AniList also exposes progress, repeat count, priority, started/completed dates and notes. Scenic should preserve similarly useful concepts while keeping its own provider-independent schema.

Reference:
- https://docs.anilist.co/reference/object/medialist

## 2.4 Progress is a core competitive behavior

Current tracking products emphasize:

- progress
- continue watching
- missed episodes
- release awareness
- history
- lists
- rewatch/status management

Scenic should not reduce its identity to recommendation AI. Accurate, explainable tracking is the data foundation on which its intelligence depends.

---

# 3. Tracking hierarchy

Scenic should support both **hierarchies** and **relationships**.

A possible hierarchy:

```text
Universe
  |
  +-- Saga / Era / Chapter / Timeline
        |
        +-- Phase / Arc / Subcollection
              |
              +-- Franchise / Series Group
                    |
                    +-- Title
                          |
                          +-- Season
                                |
                                +-- Episode
```

Not every franchise uses every level.

Examples:

```text
Marvel Cinematic Universe
  -> Saga
    -> Phase
      -> Movie or Series
        -> Season
          -> Episode
```

```text
DC
  -> DCU continuity
    -> Chapter
      -> Movie or Series

DC
  -> DCEU continuity
    -> Title

DC
  -> Arrowverse
    -> Series
      -> Season
        -> Episode
```

Anime may instead use a graph:

```text
Original Series
  -> Sequel
  -> Side Story
  -> Movie
  -> Spin-off
  -> Alternative Version
```

A title may belong to **multiple groups** at once.

---

# 4. Recommended data model

## 4.1 CollectionNode

Use a generic hierarchical entity rather than separate MarvelPhase, DCSaga, etc.

Suggested fields:

```text
CollectionNode
- id
- slug
- name
- kind
- parentId nullable
- rootId
- description
- orderingPolicy
- version
- status
- sourceType
- sourceReference
- isCurated
- createdAt
- updatedAt
```

Possible `kind` values:

```text
UNIVERSE
CONTINUITY
SAGA
ERA
PHASE
CHAPTER
ARC
FRANCHISE
SUBFRANCHISE
COLLECTION
STORYLINE
ANIME_FRANCHISE
CUSTOM_CURATED
```

The enum can evolve. Avoid assuming every provider or franchise uses the same terminology.

---

## 4.2 CollectionMembership

A title may appear in multiple collections.

Suggested fields:

```text
CollectionMembership
- collectionId
- titleId
- membershipType
- isRequired
- releasePosition nullable
- chronologicalPosition nullable
- recommendedPosition nullable
- displayPosition nullable
- continuityLabel nullable
- notes nullable
- sourceType
- sourceReference nullable
```

Examples:

- a Spider-Man movie may belong to a Spider-Man subfranchise and a broader universe
- a TV series may belong to a universe and a phase/chapter
- an anime movie may be part of a franchise but optional to the main story

---

## 4.3 TitleRelation

Use explicit relationships between titles.

Suggested fields:

```text
TitleRelation
- id
- fromTitleId
- toTitleId
- relationType
- sourceType
- sourceReference nullable
- confidence nullable
- notes nullable
```

Suggested relation types:

```text
PREQUEL
SEQUEL
PARENT
SIDE_STORY
SPIN_OFF
SAME_UNIVERSE
CROSSOVER
REBOOT
ALTERNATE_CONTINUITY
ALTERNATIVE_VERSION
ADAPTATION
SUMMARY
COMPILATION
CONTAINS
REMAKE
OTHER
```

This is especially important for anime, reboots and shared universes.

---

## 4.4 WatchOrder

A universe can have several valid orders.

```text
WatchOrder
- id
- collectionId
- name
- type
- description
- version
- sourceType
- isDefault
```

Types:

```text
RELEASE
CHRONOLOGICAL
RECOMMENDED
STORY
CUSTOM_CURATED
USER_CUSTOM
```

```text
WatchOrderItem
- watchOrderId
- itemType
- titleId nullable
- episodeId nullable
- collectionNodeId nullable
- position
- optional
- note nullable
```

This supports cases where a special watch order requires an individual episode, special, short, or nested collection.

---

# 5. Personal tracking state

Scenic should distinguish **catalog structure** from **user state**.

Recommended title-level user status:

```text
PLANNING
WATCHING
COMPLETED
PAUSED
DROPPED
REWATCHING
```

Supporting user fields may include:

```text
UserTitleState
- userId
- titleId
- status
- startedAt
- completedAt
- lastActivityAt
- repeatCount
- personalPriority
- notes
```

For movies, each actual viewing should eventually be represented as a watch event rather than permanently limiting a movie to one completion record.

For series/anime, authoritative episode watch events remain the most reliable progress source.

---

# 6. Watch event model

For robust long-term tracking, Scenic should evolve from "one MovieWatch row forever" toward an event model.

```text
WatchEvent
- id
- userId
- titleId
- seasonId nullable
- episodeId nullable
- watchedAt
- source
- eventType
- rewatchIndex nullable
- createdAt
```

Possible event types:

```text
WATCHED
UNWATCHED / CORRECTION
PROGRESS_IMPORT
REWATCHED
```

Implementation may still use simplified MVP tables initially, but the product architecture should not make rewatches impossible later.

---

# 7. Universe / franchise progress

A collection detail page should compute progress from authoritative user tracking.

## Core metrics

Show at minimum:

- released titles completed / eligible released titles
- movies completed / eligible movies
- series completed / eligible series
- seasons completed
- episodes watched / eligible episodes
- remaining episodes
- estimated watched runtime
- estimated remaining runtime
- last activity
- next unwatched item in chosen order

Example:

```text
Marvel Cinematic Universe

Released title progress
31 / 42 titles completed

Movies
24 / 28

Series
7 / 14
112 / 148 eligible episodes watched

Estimated runtime
~86h watched
~29h remaining

Current order
Release Order

Next
[Next eligible title]
```

---

# 8. Do not hide mixed-media complexity behind one percentage

A two-hour film and a 60-episode series should not silently receive identical weight without explanation.

Scenic may provide multiple progress measures:

### Title completion

```text
completed required titles / released required titles
```

This is easy to understand, but a series counts as one title only after its completion policy is satisfied.

### Episode completion

Useful for TV/anime-heavy collections.

```text
watched eligible episodes / eligible episodes
```

### Runtime completion

Estimated from known runtimes.

```text
known watched minutes / known eligible minutes
```

### Displayed overall completion

If Scenic presents one overall percentage, the UI must state the policy, for example:

> 74% by released required titles

or:

> 81% by estimated runtime

Do not present a percentage with an undefined denominator.

---

# 9. Eligibility and denominator rules

Universe progress changes when new content releases.

Therefore store or compute a clear eligibility policy.

Possible modes:

- **Released only** — recommended default
- **Released + currently airing**
- **All announced titles**
- **Main canon only**
- **Main canon + optional/spin-offs**
- **User-custom inclusion**

Future announced items should normally be shown separately rather than reducing today's completion percentage.

Example:

```text
Released completion: 100%
31 / 31 released required titles

Upcoming: 4 announced
```

This is clearer than showing 88% because four unreleased titles exist.

---

# 10. Canon, continuity and versioning

Franchise membership can change.

Scenic therefore needs:

- versioned collection definitions
- source/reference notes
- effective dates or revision history where useful
- stable internal collection IDs
- a way to mark disputed/optional membership
- a way to mark separate continuities

Do not merge distinct DC continuities into one "DC Universe completion" denominator unless the user intentionally selects such a custom meta-collection.

Examples that should remain independently trackable:

- DCU
- DCEU
- Arrowverse
- Elseworlds / separate continuities

Likewise, an MCU collection may coexist with Marvel subfranchises and other Marvel continuities.

---

# 11. Franchise / Universe pages

## 11.1 Universe Hub

Purpose: browse major trackable collections.

Sections:

- Continue a Universe
- Nearly Complete
- Recently Updated
- Marvel
- DC
- Star Wars
- Wizarding World
- Anime Franchises
- Other Franchises
- My Pinned Universes

Filters:

- movie
- series
- anime
- mixed media
- completed
- in progress
- not started
- release order available
- chronological order available

---

## 11.2 Universe Detail

Show:

- artwork / identity
- description
- selected continuity
- released completion
- upcoming count
- movies/series/episodes breakdown
- estimated remaining runtime
- chosen watch order
- next item
- hierarchy tree
- saga/phase/chapter cards
- timeline/order switcher
- watched/unwatched filters
- optional items toggle
- stats
- AI actions such as "plan my catch-up"

---

## 11.3 Saga / Phase / Chapter Detail

Show:

- parent universe
- ordered titles
- progress
- remaining runtime
- completion state
- next item
- upcoming titles
- child groups

---

## 11.4 Watch Order page

Allow switching among:

- Release Order
- Chronological Order
- Recommended Order
- Custom Order

Each row should show:

- title
- year/date
- media type
- completion state
- progress if series
- runtime / commitment
- optional/main indicator
- reason/note for unusual placement

---

## 11.5 Title Detail integration

A title detail page can show:

```text
Part of:
Marvel Cinematic Universe
-> Multiverse Saga
-> Phase ...

Also part of:
[Subfranchise]
```

Actions:

- View universe
- View watch order
- Mark watched
- Update progress
- See next related title

---

# 12. Tracking pages related to this subsystem

The franchise/universe system connects to:

| Page | Tracking role |
|---|---|
| Home | Continue universes; catch-up cards |
| Library | Filter by universe/franchise/status |
| History | Show watches within franchise context |
| Continue Watching | Resume active series inside a collection |
| Universe Hub | Browse tracked universes |
| Universe Detail | Full progress and hierarchy |
| Saga/Phase/Chapter Detail | Nested progress |
| Watch Order | Ordered completion workflow |
| Movie Detail | Collection memberships |
| Series Detail | Collection memberships + episode progress |
| Anime Detail | Relation graph + franchise progress |
| Calendar / Upcoming | Upcoming items within followed universes |
| Statistics | Universe/franchise/filmography analytics |
| Goals | Catch-up / completion goals |
| Ask Scenic | Natural-language queries over structured progress |

---

# 13. API design

Proposed public API additions:

```text
GET  /collections
GET  /collections/:id
GET  /collections/:id/tree
GET  /collections/:id/items
GET  /collections/:id/orders
GET  /collections/:id/orders/:orderId
GET  /titles/:id/collections
GET  /titles/:id/relations

GET  /me/collections
GET  /me/collections/:id/progress
GET  /me/collections/:id/next
GET  /me/collections/:id/stats
PUT  /me/collections/:id/preferences

GET  /me/titles/:titleId/state
PUT  /me/titles/:titleId/state
```

Optional later endpoints:

```text
POST /me/collections/:id/custom-order
POST /me/collections/:id/goals
GET  /me/collections/:id/catch-up-plan
```

The API should return:

- collection version
- progress policy
- eligible count
- completed count
- upcoming count
- selected watch order
- next item
- child progress summaries

---

# 14. Example progress response

```json
{
  "collectionId": "mcu",
  "collectionVersion": 12,
  "policy": {
    "eligibility": "RELEASED_REQUIRED",
    "completionMetric": "TITLE"
  },
  "progress": {
    "eligibleTitles": 42,
    "completedTitles": 31,
    "titlePercent": 73.81,
    "eligibleEpisodes": 148,
    "watchedEpisodes": 112,
    "episodePercent": 75.68,
    "knownRuntimeMinutes": 6900,
    "watchedRuntimeMinutes": 5100,
    "runtimePercent": 73.91
  },
  "upcomingTitles": 4,
  "next": {
    "titleId": "title_123",
    "order": "RELEASE"
  }
}
```

Percentages above are illustrative only.

---

# 15. AI integration

The Python intelligence service **does not own collection truth**.

The main backend supplies:

- collection hierarchy
- memberships
- watch order
- user progress
- remaining runtime
- upcoming release context

AI may answer:

- "How much of the MCU have I completed?"
- "What Marvel titles am I missing?"
- "What should I watch next in release order?"
- "Can I finish this phase over the weekend?"
- "How long will it take to catch up before the next release?"
- "Which DC continuity am I closest to completing?"
- "Give me a spoiler-safe recap before I continue."
- "Which Naruto spin-offs are optional?"
- "What anime in this franchise haven't I watched?"

AI should never invent collection membership or canon status. It must use Scenic's curated data.

---

# 16. Recommendation integration

Universe data can become a recommendation signal.

Examples:

- user is 1 title away from completing a phase
- new season starts soon
- user has a sequel unwatched after completing the previous title
- collection title is leaving a subscribed service
- user asked to continue an active franchise
- user has explicitly excluded a universe

Possible reason codes:

```text
FRANCHISE_CONTINUATION
PHASE_NEAR_COMPLETION
SAGA_NEAR_COMPLETION
SEQUEL_READY
NEW_SEASON_CATCHUP
UNIVERSE_INTEREST
WATCH_ORDER_NEXT
COLLECTION_GOAL
```

---

# 17. Statistics

Potential franchise statistics:

- universes started
- universes completed
- phases/chapters completed
- franchises completed
- movies completed per universe
- episodes completed per universe
- rewatch count
- total runtime by universe
- completion by year
- longest-running active franchise
- closest-to-completion collection
- most watched franchise
- highest-rated franchise
- most rewatched franchise

Filmography progress can use a similar generic collection mechanism where appropriate, but actor/director filmography is better derived from credits than manually curated universe membership.

---

# 18. Notifications and upcoming releases

Users may follow:

- a universe
- saga
- phase/chapter
- franchise
- individual title
- series

Possible notifications:

- new movie announced
- release date changed
- new season announced
- episode released
- trailer released
- watch-provider availability changed
- next phase/chapter item released
- catch-up reminder before a release

Notifications should be preference-driven and must not expose unreliable provider data as certain.

---

# 19. Import and provider mapping

When importing from another tracker:

1. resolve external title IDs to Scenic canonical titles
2. preserve watch dates where available
3. preserve episode progress
4. preserve rewatch counts where reliable
5. derive collection/universe progress from Scenic's current collection graph
6. show unresolved matches and confidence
7. never silently guess ambiguous titles

Universe progress should be **derived** after import rather than imported as an opaque percentage.

---

# 20. Curation strategy

Provider data can seed relationships, but Scenic should have a curation layer.

A collection revision should record:

- what changed
- source/reason
- who/what produced the change
- previous version
- effective timestamp

Do not let a provider refresh automatically destroy or radically reinterpret users' historical progress.

Recommended approach:

```text
Provider data
   |
   v
Normalization / mapping
   |
   v
Scenic curated collection graph
   |
   v
Versioned collection definitions
   |
   v
Derived personal progress
```

---

# 21. MVP vs full product scope

## Academic/core MVP

Keep the implementation achievable:

- movie watch history
- episode-level series/anime progress
- season progress
- basic statuses
- one curated demonstration universe/collection
- one order
- derived completion
- tests

A Marvel sample can be useful because it demonstrates mixed movie/series hierarchy.

## Next product phase

- multiple universes
- multiple orders
- DC continuity separation
- anime relation graph
- optional/main membership
- runtime progress
- upcoming/release integration
- rewatch events
- collection goals

## Later

- collaborative curation tools
- import reconciliation UI
- sophisticated canon/version handling
- user-created public watch orders
- provider/subscription urgency
- group universe catch-up planning

---

# 22. Acceptance tests

At minimum test:

- a title may belong to multiple collections
- child collection progress rolls up correctly
- unreleased titles do not reduce released-only completion
- optional titles are excluded when policy says main-only
- series completion reflects eligible episode state
- a new released episode can change an ongoing series from up-to-date to incomplete
- different watch orders do not change watched history
- switching order changes only next-item calculation
- DCEU and DCU progress stay independent
- a reboot/alternate continuity does not silently merge progress
- imported watches correctly derive collection progress
- rewatching does not inflate first-completion counts
- missing runtime does not become zero-duration watched progress
- collection revision does not delete user history
- cross-user authorization protects personal progress
- AI cannot return an unknown collection/title ID as authoritative

---

# 23. UI rules

- Always state the progress denominator/policy.
- Separate released content from upcoming content.
- Distinguish **up to date** from **fully ended/completed**.
- Do not call an ongoing universe "fully complete forever."
- Do not silently mix separate continuities.
- Show optional/spin-off items clearly.
- Preserve user's selected watch order.
- Make "what is next?" obvious.
- Keep mark-watched / mark-season / watch-until-here actions fast.
- Support undo for bulk tracking changes.

---

# 24. Scenic tracking principle

The data hierarchy should let Scenic answer all of these without guessing:

```text
What have I watched?
Where did I stop?
What am I watching now?
What did I drop?
What am I rewatching?
What is next?
What am I missing?
How much of this universe have I completed?
How long is left?
Which order am I following?
What is optional?
What is newly released?
What should I finish before the next release?
```

That tracking foundation becomes input to Scenic's Memory, Taste and Decision systems.

---

## Related documentation

- `PROJECT.md`
- `docs/REQUIREMENTS.md`
- `docs/DATA_MODEL.md`
- `docs/API.md`
- `docs/ARCHITECTURE.md`
- `docs/AI_SYSTEM_HANDOFF.md`
- `docs/DECISION_ENGINE.md`

---

**Status:** Product architecture / tracking specification  
**Last updated:** 2026-09-29
