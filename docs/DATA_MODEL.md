# Proposed data model

All identifiers below are internal IDs unless labeled provider IDs. Use UTC timestamps and explicit foreign keys.

| Entity | Important fields | Rules |
|---|---|---|
| User | id, normalizedEmail, passwordHash or authSubject, createdAt | Unique normalized email/auth subject; never expose passwordHash |
| Title | id, provider, providerId, type, name, overview, runtimeMinutes | Unique provider + type + providerId |
| Genre | id, name | Stable normalized identifier |
| TitleGenre | titleId, genreId | Composite unique key |
| Season | id, titleId, seasonNumber | Unique title + season number |
| Episode | id, seasonId, episodeNumber, airDate, runtimeMinutes | Unique season + episode number |
| WatchlistEntry | userId, titleId, createdAt | Composite unique key |
| MovieWatch | userId, titleId, watchedAt | One completion per user/movie in MVP |
| EpisodeWatch | userId, episodeId, watchedAt | One completion per user/episode |
| Rating (P1) | userId, titleId, value | Unique user/title; agreed bounded scale |
| Collection (P1) | id, name, orderingPolicy, version | Curated membership/version |
| CollectionItem (P1) | collectionId, titleId, position | Unique collection/title and collection/position |

## Invariants
MovieWatch accepts only movie titles. Episodes belong to series through seasons. API service validation enforces cross-table type rules; add database constraints where practical.
Viewing operations use upserts/unique keys so retries cannot duplicate completion.
Catalog refresh must not delete user history; use stable provider mappings and soft retirement of missing metadata.
Account deletion removes or anonymizes related personal records according to the agreed policy.

## Statistics definitions
- Watched movies: distinct movie IDs in MovieWatch.
- Watched episodes: distinct episode IDs in EpisodeWatch.
- Eligible episodes: aired regular episodes on the evaluation date; exclude specials/season 0 by default. Unknown air dates are excluded and shown as incomplete metadata.
- Completed season: has at least one eligible episode and all eligible episodes are watched.
- Up-to-date series: has at least one eligible episode and all eligible episodes are watched. Label this “up to date” for ongoing shows.
- Genre distribution: distinct completed movies and up-to-date series grouped by genre; multi-genre titles count in each category.
- Watch time, if added: sum only known runtimes and label the result an estimate.

Include evaluation date and metadata limitations where needed. A new aired episode can make an ongoing series no longer up to date.
