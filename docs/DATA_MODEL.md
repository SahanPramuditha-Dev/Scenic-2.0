# Proposed data model

All identifiers below are internal IDs unless labeled provider IDs. Use UTC timestamps and explicit foreign keys.

| Entity | Important fields | Rules |
|---|---|---|
| User | id, normalizedEmail, passwordHash or authSubject, createdAt | Unique normalized email/auth subject; never expose passwordHash |
| Title | id, provider, providerId, type, domain, name, overview, runtimeMinutes | Unique provider + type + providerId; domain may distinguish anime presentation without making provider IDs authoritative |
| Genre | id, name | Stable normalized identifier |
| TitleGenre | titleId, genreId | Composite unique key |
| Season | id, titleId, seasonNumber | Unique title + season number |
| Episode | id, seasonId, episodeNumber, airDate, runtimeMinutes | Unique season + episode number |
| WatchlistEntry | userId, titleId, createdAt | Composite unique key |
| MovieWatch | userId, titleId, watchedAt | One completion per user/movie in MVP |
| EpisodeWatch | userId, episodeId, watchedAt | One completion per user/episode |
| Rating (P1) | userId, titleId, value | Unique user/title; agreed bounded scale |
| UserTitleState (P1) | userId, titleId, status, startedAt, completedAt, repeatCount, personalPriority | Status is planning/watching/completed/paused/dropped/rewatching; state does not replace granular watch history |
| CollectionNode (P1) | id, slug, name, kind, parentId, rootId, version, orderingPolicy, sourceType | Generic hierarchy for universe/continuity/saga/phase/chapter/arc/franchise/collection; no Marvel/DC-specific tables |
| CollectionMembership (P1) | collectionId, titleId, isRequired, releasePosition, chronologicalPosition, recommendedPosition, continuityLabel | A title may belong to multiple groups; optional/main-story membership is explicit |
| WatchOrder (P1) | id, collectionId, name, type, version, isDefault | Supports release, chronological, recommended, curated and later user-custom orders |
| WatchOrderItem (P1) | watchOrderId, titleId or episodeId or collectionNodeId, position, optional | Ordered leaf/nested item; exactly one target kind per row |
| TitleRelation (P1) | fromTitleId, toTitleId, relationType, sourceType, confidence | Models sequel/prequel/spin-off/same-universe/reboot/alternate-continuity/etc. |
| WatchEvent (future) | id, userId, titleId, seasonId, episodeId, watchedAt, eventType, rewatchIndex | Event-oriented history supports repeated watches and imports; simplified MVP MovieWatch/EpisodeWatch may remain initially |

## Invariants
MovieWatch accepts only movie titles. Episodes belong to series through seasons. API service validation enforces cross-table type rules; add database constraints where practical.
Viewing operations use upserts/unique keys so retries cannot duplicate completion.
Catalog refresh must not delete user history; use stable provider mappings and soft retirement of missing metadata.
Provider collection IDs are metadata inputs, not Scenic's authoritative universe model. Curated collection nodes and relations are versioned independently.
Collection progress is derived from canonical watch history; never store a standalone percentage as the source of truth.
Watch-order changes never mutate watch events.
Separate continuities remain separate roots/subtrees unless a curated parent explicitly combines them.
Account deletion removes or anonymizes related personal records according to the agreed policy.

## Statistics definitions
- Watched movies: distinct movie IDs in MovieWatch.
- Watched episodes: distinct episode IDs in EpisodeWatch.
- Eligible episodes: aired regular episodes on the evaluation date; exclude specials/season 0 by default. Unknown air dates are excluded and shown as incomplete metadata.
- Completed season: has at least one eligible episode and all eligible episodes are watched.
- Up-to-date series: has at least one eligible episode and all eligible episodes are watched. Label this “up to date” for ongoing shows.
- Genre distribution: distinct completed movies and up-to-date series grouped by genre; multi-genre titles count in each category.
- Watch time, if added: sum only known runtimes and label the result an estimate.
- Released collection title progress: completed required released titles / required released titles under the selected collection version.
- Collection episode progress: watched eligible episodes / eligible episodes for member series under the stated policy.
- Collection runtime progress: known watched runtime / known eligible runtime; label as an estimate and exclude unknown runtime from the denominator rather than treating it as zero.
- Upcoming collection items: announced/unreleased items are counted separately by default and do not reduce released-only completion.

Include evaluation date and metadata limitations where needed. A new aired episode can make an ongoing series no longer up to date.


## Franchise model detail
See `FRANCHISE_UNIVERSE_TRACKING.md` for hierarchy, relation graph, watch-order, curation/versioning and mixed-media progress rules.
