# Scenic 2.0 — Context-Aware Recommendation & Decision Intelligence

> **Purpose:** Define Scenic's product-level recommendation behavior beyond the academic deterministic baseline.
>
> **Core principle:** A title can be an excellent taste match and still be the wrong recommendation **right now**.
>
> Scenic should decide using both long-term taste and short-lived session context.

---

## 1. Product goal

Scenic should answer questions such as:

- "I have about 40 minutes before bed. What should I watch?"
- "Give me something Matrix-like for a short break."
- "I usually like MCU content. What fits tonight?"
- "I have three hours now; give me a movie."
- "Continue something I already started."
- "What should I watch before the next Avengers movie?"
- "I don't want horror tonight, but don't remove horror from my preferences."
- "That suggestion is good, just too long for now."

The system must avoid reducing recommendation to a single generic similarity score.

---

## 2. Recommendation model

Scenic separates two major questions:

### 2.1 Taste Match

> Would this user probably enjoy this title?

Possible signals:

- genre/theme affinity
- people/studio/director affinity
- franchise/universe affinity
- ratings and favorites
- completions vs drops
- rewatches
- historical recommendation feedback
- recent interests
- similarity to highly rated titles
- novelty/exploration preference

### 2.2 Context Match

> Is this a good choice for the user's current situation?

Possible signals:

- available time
- remaining runtime for in-progress titles
- bedtime / break / weekend / family / friends context
- mood
- energy
- desired commitment
- movie vs episode preference
- alone vs group
- streaming availability
- whether the user wants something familiar or new
- franchise goal / upcoming release pressure
- spoiler-safe progress position

A recommendation should normally satisfy both.

---

## 3. Session Context

A recommendation request may include a temporary SessionContext.

Suggested fields:

```text
SessionContext
- availableMinutes nullable
- timeToleranceMinutes nullable
- modeId nullable
- moodTags[]
- energyLevel nullable
- commitmentLevel nullable
- preferredMediaTypes[]
- companyContext nullable
- familiarityPreference nullable
- continueExistingPreference nullable
- allowedProviders[]
- excludedGenres[]
- excludedTitles[]
- franchiseFocusId nullable
- goalId nullable
- startedAt
- expiresAt nullable
```

Session context should not automatically mutate permanent taste.

Example:

> "No horror tonight"

means a temporary exclusion.

Example:

> "I don't like horror"

is a long-term preference signal.

---

## 4. Watch Modes

Users may save reusable contexts.

Suggested built-in examples:

### Bedtime

- approximately 30–50 minutes
- low commitment
- episodes preferred
- unfinished titles preferred
- avoid starting long movies

### Quick Break

- approximately 15–45 minutes
- low commitment
- easy stopping point
- short episode / anthology / short-form content preferred

### Weekend

- longer available time
- movies and high-commitment titles allowed
- broader exploration

### Family

- family-safe restrictions
- shared/family taste profile
- explicit content boundaries

### With Friends

- group compatibility
- easy-to-agree choices
- shared availability/provider constraints

Users should be able to create custom modes.

Automatic routine learning may be introduced later, but Scenic should not silently create permanent preferences from time-of-day patterns without user control.

---

## 5. Taste Modes / Contextual Taste Profiles

One user can have different viewing contexts without corrupting their main profile.

Examples:

```text
Personal
- cyberpunk
- psychological sci-fi
- mystery
- dark thrillers

Family
- Marvel
- animation
- adventure
- comedy

Friends
- horror
- action
- comedy
```

Suggested model:

```text
TasteProfile
- id
- userId
- name
- type: PERSONAL | FAMILY | FRIENDS | CUSTOM
- isDefault
- createdAt
- updatedAt
```

Signals may belong to the default personal profile or a selected contextual profile.

---

## 6. Effective Watch Time

Runtime filtering must use the time the user actually needs now.

For an unwatched movie:

```text
effectiveWatchTime = fullRuntime
```

For an in-progress movie:

```text
effectiveWatchTime = fullRuntime - watchedProgress
```

For a series:

```text
effectiveWatchTime = nextEpisodeRuntime
```

For a multi-episode suggestion:

```text
effectiveWatchTime = sum(selectedEpisodeRuntimes)
```

Example:

A 169-minute movie normally fails a 40-minute request.

If only 35 minutes remain, it may become one of the strongest choices.

The system should distinguish **title runtime** from **remaining commitment**.

---

## 7. Time-Fit Logic

Time should be a strong constraint when explicitly provided.

Possible policy:

- exact fit: within requested time
- near fit: within configurable tolerance
- over-limit candidate: allowed only when clearly explained and alternatives are weak
- long-form deferral: preserve high taste-match titles for a later queue

Example:

> "Blade Runner 2049 strongly matches your taste, but it is too long for tonight. Saved to Weekend."

The AI should be able to recommend **not watching a specific title now** without treating that as dislike.

---

## 8. Smart Queue Lanes

Instead of one flat watchlist, Scenic can organize candidates dynamically.

Suggested lanes:

- **Now**
- **Tonight**
- **Weekend**
- **Later**
- **Continue**
- **Catch-Up**
- **Leaving Soon** (only when provider data is reliable)

A title may move between lanes based on:

- available time
- current progress
- upcoming release
- watchlist age
- user priority
- provider availability
- franchise goals
- recent interest
- session context

Queue ranking must remain explainable.

---

## 9. Recommendation scoring

The product should not lock itself to one permanent formula.

A future score can combine normalized components such as:

```text
finalScore =
    tasteFit
  + contextFit
  + timeFit
  + progressContinuation
  + watchlistPriority
  + franchiseRelevance
  + moodFit
  + availabilityFit
  + freshness
  + explicitPositiveFeedback
  + explorationBonus
  - runtimeMismatch
  - repeatedDismissalPenalty
  - hardConstraintPenalty
```

Weights are hypotheses and must be evaluated.

Hard constraints should be handled before ranking where possible.

---

## 10. Why This? and Why Now?

Every recommendation should provide an explanation based on real signals.

Examples:

> Because you rated The Matrix highly and often complete cyberpunk sci-fi.

> Fits your 40-minute bedtime session.

> You are already halfway through this episode.

> Continues your MCU watch order.

> You are one title away from completing this phase.

> Available on one of your selected services.

Scenic should also support **Why later?**

Example:

> Strong taste match, but 2h 44m is a poor fit for this session. Added to Weekend.

This is a key differentiator from simple similarity feeds.

---

## 11. Temporary vs Permanent Feedback

Feedback must preserve intent.

### Temporary/session feedback

- Not tonight
- Too long
- Wrong mood
- Too intense right now
- Want something new
- Continue something instead

These signals should primarily affect the current session or short-term ranking.

### Long-term feedback

- Not interested
- I dislike this genre/theme
- Never recommend this title
- More like this
- Less like this
- Favorite
- High rating
- Rewatch

These may update long-term preference models.

The UX must not treat every rejection as a dislike.

---

## 12. Recommendation Sandbox

After a result is shown, the user should refine it without restarting.

Suggested actions:

- Shorter
- Longer
- Newer
- Older
- Darker
- Lighter
- More action
- More sci-fi
- Less violent
- More like this
- Less like this
- Something already started
- Something completely different
- Only my streaming services
- Surprise me

Each refinement should update the SessionContext and rerank candidates.

---

## 13. Exploration Control

Users should control how adventurous the recommender is.

Possible scale:

```text
Familiar <--------------------> Surprise me
```

Low exploration:
- known genres
- active franchises
- similar creators
- familiar themes

High exploration:
- new genres
- international content
- lesser-known titles
- hidden gems
- adjacent tastes

This should be explicit rather than silently forcing novelty.

---

## 14. Post-Watch Micro Feedback

Scenic should collect richer signals without demanding full reviews.

Example:

```text
How was it?
- Loved it
- Good
- Okay
- Didn't like it

What stood out?
- Story
- World
- Characters
- Action
- Visuals
- Philosophy
- Soundtrack

What did not work?
- Slow
- Too long
- Confusing
- Predictable
```

Responses are optional.

Micro feedback can improve recommendations more efficiently than star ratings alone.

---

## 15. Editable Entertainment DNA

Scenic should expose what it believes about the user's taste.

Example:

```text
Sci-Fi               Very High
Cyberpunk            Very High
Mystery              High
Superhero            High
Comedy               Medium
Romance              Low confidence
```

The UI should distinguish:

- strong positive evidence
- negative evidence
- low-data / unknown areas

Important rule:

> "Has not watched much romance" must not automatically become "dislikes romance."

Users should be able to correct the model.

---

## 16. Ask Scenic behavior

Ask Scenic should act as a conversational interface over real Scenic state.

Example:

> User: I have about 40 minutes before bed.

Scenic should consider:

- current SessionContext
- active Watch Mode
- in-progress titles
- next-episode runtimes
- Taste Profile
- watchlist
- franchise progress
- streaming availability
- explicit exclusions
- spoiler boundary

Possible response structure:

```text
Best fit
[Title / episode]
~42 min

Why now
- matches your recent MCU viewing
- continues an active series
- close to your available time

Alternative
[Another title]
~39 min

Saved for later
[Long movie]
- strong taste match, but too long for tonight
```

---

## 17. Recommendation memory

Scenic should remember prior recommendation interactions.

Users may ask:

- "What was that movie you suggested yesterday?"
- "Show me the sci-fi recommendation I skipped."
- "Why did you recommend this?"
- "Give me the other option from last time."

Suggested model:

```text
RecommendationSession
- id
- userId
- tasteProfileId nullable
- watchModeId nullable
- sessionContextSnapshot
- createdAt

RecommendationResult
- sessionId
- titleId
- rank
- scoreComponents
- explanationCodes[]
- disposition: SHOWN | ACCEPTED | DISMISSED | DEFERRED | WATCHED
```

This also supports offline evaluation and reproducibility.

---

## 18. Streaming-aware decision making

When provider availability exists and the user has selected services, availability should affect recommendations.

Example:

> Only show things I can watch with my current subscriptions.

Do not make strong availability claims when provider data is stale or unavailable.

Availability is a ranking/eligibility signal, not a substitute for taste.

---

## 19. Universe / franchise intelligence

Franchise data is not only for progress bars.

The decision layer can use:

- active universe interest
- next item in selected watch order
- phase/saga near completion
- sequel readiness
- upcoming new season/movie
- required story dependencies
- catch-up goals

Suggested reason codes:

```text
FRANCHISE_CONTINUATION
WATCH_ORDER_NEXT
PHASE_NEAR_COMPLETION
SAGA_NEAR_COMPLETION
SEQUEL_READY
UPCOMING_RELEASE_CATCHUP
COLLECTION_GOAL
```

---

## 20. Story dependency intelligence

Scenic may classify curated prerequisites for a target title.

Suggested dependency importance:

- **Required** — important for core continuity
- **Helpful** — improves context but not strictly necessary
- **Optional** — side story / enrichment
- **Avoid for spoilers** — later content that should not be surfaced before the target

Example:

```text
Before [Target Movie]

Required
- Title A
- Series B Season 1

Helpful
- Special C

Optional
- Spin-off D
```

These classifications must come from curated Scenic data or a trusted source layer, not AI invention.

---

## 21. Release-driven catch-up planning

If a target release date is known:

```text
remainingRuntime / remainingDays
```

can estimate required pace.

Example:

```text
17h 20m remaining
21 days left
≈ 50 minutes/day
```

Plans may be generated around:

- weekdays/weekends
- user's preferred Watch Modes
- episode/movie boundaries
- required vs optional content

---

## 22. Spoiler-aware recommendation rules

A recommendation must respect the user's tracked progress.

The AI should not:

- reveal future episode events
- expose late-series character states
- recommend a recap containing future material
- explain a franchise dependency using spoilers beyond the user's position

Spoiler boundaries are product data, not optional conversational behavior.

---

## 23. Vague-memory / personal semantic search

Ask Scenic should support queries like:

- "What was that movie with red and blue pills?"
- "That train movie where the same event repeats."
- "Who was the actress from the Marvel show I watched last month?"

The differentiator is not semantic search alone; it is semantic search combined with the user's own history and current Scenic state.

---

## 24. Cold start

For a new user:

1. explicit onboarding interests
2. a few liked/disliked known titles
3. optional import from existing history
4. provider popularity/rating as a fallback
5. transparent low-confidence explanations

Scenic should avoid pretending it knows a user's taste before enough evidence exists.

---

## 25. Evaluation

The AI/recommendation team should test scenario fixtures, not only random title lists.

Minimum scenarios:

1. 40-minute bedtime + MCU fan + active 42-minute episode
2. 40-minute break + Matrix-like taste + no suitable movie
3. 40-minute request + 35 minutes remaining in an in-progress long movie
4. "Not tonight" feedback does not become permanent dislike
5. "Never recommend this" persists across sessions
6. family mode excludes disallowed content
7. weekend mode allows long-form high-taste candidates
8. selected provider filter removes unavailable titles
9. franchise catch-up promotes required items
10. spoiler boundary prevents unsafe explanation
11. cold-start user receives transparent fallback
12. recommendation reranking responds correctly to "shorter" / "something new"

Metrics to record where practical:

- constraint satisfaction rate
- explanation correctness
- acceptance/click-through in test sessions
- inappropriate-over-time recommendation rate
- repeat-dismissal rate
- fallback rate
- p95 decision latency
- deterministic reproducibility for baseline fixtures

Do not claim recommendation accuracy improvement without a defined dataset and comparison method.

---

## 26. Service ownership

### Main Scenic backend owns

- user history
- title/episode progress
- watchlist
- Watch Modes
- Taste Profiles and user-selected preferences
- franchise/universe truth
- provider/subscription settings
- recommendation interaction history
- authorization

### Python intelligence service owns

- feature extraction
- ranking
- reranking
- contextual scoring
- explanation assembly from verified signals
- optional future ML models

### Frontend owns

- context capture
- Watch Mode selection
- recommendation refinement controls
- explanation display
- queue lane UX
- feedback UX

The AI service must not become the source of truth for user progress, canon, collection membership or availability.

---

## 27. Suggested API contracts

Possible endpoints:

```text
GET    /me/watch-modes
POST   /me/watch-modes
PATCH  /me/watch-modes/:id
DELETE /me/watch-modes/:id

GET    /me/taste-profiles
POST   /me/taste-profiles
PATCH  /me/taste-profiles/:id

POST   /me/decisions
POST   /me/decisions/:sessionId/refine
POST   /me/decisions/:sessionId/feedback
GET    /me/decisions/history
GET    /me/decisions/:sessionId

GET    /me/smart-queue
PATCH  /me/smart-queue/:titleId

GET    /me/collections/:id/catch-up-plan
POST   /me/collections/:id/catch-up-plan
```

Exact contracts should be finalized in `API.md` before implementation.

---

## 28. Suggested implementation phases

### Academic MVP

Keep the deterministic baseline in `DECISION_ENGINE.md`.

### P1 — Context-aware product layer

- explicit available-time input
- remaining-runtime awareness
- Watch Next
- explainable "why now"
- temporary vs permanent feedback
- Smart Queue
- Watch Modes
- selected Taste Profile
- franchise continuation signals

### P2 — Conversational intelligence

- Ask Scenic
- Recommendation Sandbox
- recommendation memory/history
- semantic personal search
- release-driven catch-up planner
- story dependency reasoning
- group decision
- routine-learning experiments
- future ML personalization

---

## 29. Product success principle

Scenic should not become:

> "a chatbot that knows movie titles"

or:

> "a watchlist with an AI button"

The intended experience is:

> **Scenic remembers what you watch, understands your taste, understands your current situation, and helps you make the right entertainment decision for now.**
