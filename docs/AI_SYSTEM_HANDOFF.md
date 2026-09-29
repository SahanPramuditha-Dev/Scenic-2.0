# Scenic 2.0 — AI System Handoff

> **Audience:** AI / Python developer working on Scenic 2.0  
> **Purpose:** Explain the complete Scenic product context, all AI-powered features, the pages that consume AI, and the integration boundary between the main Scenic backend and the Python intelligence service.

---

## 1. What Scenic Is

Scenic is an **entertainment tracking, discovery, and decision platform** for movies, TV series, and anime.

It is **not a streaming platform**, and its AI should not be treated as a generic chatbot.

Scenic has three core intelligence ideas:

```text
MEMORY  ->  TASTE  ->  DECISION
```

- **Memory:** Scenic remembers what the user watched, rated, dropped, rewatched, saved, and progressed through.
- **Taste:** Scenic converts that history and feedback into an evolving understanding of the user's entertainment preferences.
- **Decision:** Scenic combines taste with the user's current situation to help answer the most important question: **"What should I watch now?"**

The AI bot, recommendation engine, Scenic Match, smart watchlist, semantic search, spoiler-safe recap, and other AI features are built around these three ideas.

---

## 2. AI Feature Map

| Feature | Purpose |
|---|---|
| Scenic Decision Engine | Decide what the user should watch in the current situation |
| Personalized Recommendation Engine | Recommend movies, series, and anime based on taste |
| Ask Scenic | Natural-language interface to Scenic intelligence |
| Entertainment DNA | Build an evolving taste profile |
| Entertainment Memory | Search and reason over personal viewing history |
| Scenic Match | Calculate personalized title-to-user compatibility |
| Context Intelligence | Use mood, time, company, commitment, etc. |
| Smart Watchlist / Smart Queue | Prioritize saved titles intelligently |
| Semantic Discovery | Understand natural-language discovery requests |
| Spoiler Intelligence | Respect exactly how far a user has watched |
| Catch Me Up / Recap | Generate spoiler-safe progress-aware recaps |
| Recommendation Explanation Engine | Explain why a title was recommended |
| Feedback Learning | Learn from ratings, skips, drops, rewatches, etc. |
| Smart Continue Watching | Rank active content using context and behavior |
| AI Smart Lists | Generate personalized watch lists from instructions |
| Group Recommendation | Find content suitable for multiple users |
| AI Statistics Insights | Explain patterns found in user statistics |
| Year in Review | Convert real yearly viewing data into a narrative |
| Personalized Upcoming | Rank upcoming releases for the user |
| Franchise Intelligence | Understand progress across universes/franchises |
| Taste Evolution | Show how the user's preferences change over time |
| Hidden Gem Detector | Find high-fit, lower-popularity content |
| Comfort Zone Breaker | Recommend adjacent but meaningfully different content |
| Smart Watch Planner | Build a time-bounded viewing plan, not just one recommendation |
| Commitment Intelligence | Understand hours/episodes/seasons remaining before recommending |
| Recommendation Refinement | Let users say shorter, lighter, stranger, more obscure, etc. |
| Recommendation Memory | Remember prior recommendations, acceptance, skips, and repetition |
| Confidence / Uncertainty | Expose confidence in rankings and data freshness |
| Taste Correction | Let users correct Scenic's inferred assumptions |
| Availability Intelligence | Combine personal taste/backlog with where content is available |
| Subscription Intelligence | Analyze service coverage and optional user-entered cost/value |
| Release / Urgency Intelligence | Use leaving-soon and new-season timing in ranking |
| Social Compatibility | Compare taste profiles between two users |
| Group Watch Planner | Recommend for a group and support voting/consensus |
| Spoiler-Safe Group Intelligence | Respect the least-advanced group member's progress |
| Goal-Aware Recommendations | Help finish a season, franchise, backlog, or viewing goal |
| Smart Recommendation Modes | Safe pick, hidden gem, comfort-zone break, quick watch, surprise me |

---

# 3. Scenic Decision Engine

The Decision Engine is the **primary AI feature** of Scenic.

Its job is not to return a huge catalogue. Its job is to reduce choice.

A good Decision Engine response should normally provide **around 3 strong choices**, with transparent reasons.

### Example request

> I have around 90 minutes. I want something funny and light. I do not want to start a new series.

### Candidate structured interpretation

```json
{
  "intent": "watch_recommendation",
  "media_type": "movie",
  "max_runtime_minutes": 120,
  "moods": ["funny", "light"],
  "exclude_new_series": true,
  "exclude_watched": true
}
```

### Signals the engine may use

- available time
- mood
- movie / series / anime preference
- desired commitment
- current series progress
- user taste profile
- ratings
- favourites
- rewatches
- recent viewing
- recent genre consumption
- language preference
- intensity
- company: alone / partner / family / friends
- watchlist
- content availability
- franchise progress
- dropped titles
- recommendation feedback
- hidden/not-interested titles
- temporary context such as "not tonight"

### Important learning rule

```text
"Not tonight" != "I dislike this"
```

Temporary context rejection must not become a permanent negative preference.

---

# 4. Ask Scenic — AI Bot

Ask Scenic is the natural-language interface to the Scenic platform.

It should **call Scenic functions and query real Scenic data**, not act like an isolated general-purpose LLM.

### Example requests

| User request | Required AI behavior |
|---|---|
| "What should I watch tonight?" | Run Decision Engine |
| "Something under 2 hours." | Apply runtime/context constraint |
| "Something like Interstellar but less serious." | Semantic similarity + personalized ranking |
| "What was that Korean movie I watched last year?" | Entertainment Memory |
| "What shows did I stop watching?" | Query progress/history |
| "Why did you recommend this?" | Explanation Engine |
| "Recommend something for me and my friend." | Group recommendation |
| "I don't want horror tonight." | Apply temporary context preference |
| "Don't recommend this actor again." | Store persistent preference |
| "What Marvel movies haven't I watched?" | Franchise + history query |
| "How much of the MCU have I completed?" | Franchise progress |
| "What can I finish before 11 PM?" | Time-aware Decision Engine |
| "What are my favourite genres?" | Entertainment DNA |
| "Make me a weekend movie list." | Smart List generation |
| "What did I watch most this year?" | Stats + AI insight |

### Bot principle

The LLM should handle:
- natural-language understanding
- intent extraction
- constraint extraction
- conversational presentation
- explanation

The Scenic platform should handle:
- real user data
- title catalogue
- progress
- ratings
- watch history
- availability
- candidate retrieval
- validated actions

---

# 5. Entertainment Memory

Entertainment Memory lets users search their own entertainment history naturally.

Examples:

> "What was that movie I watched around Christmas where the main character was stuck in a hotel?"

> "What sci-fi movies did I watch in 2025?"

> "Which anime did I rate above 8?"

> "What was the series I stopped after season 2?"

This requires a combination of:

1. structured history queries
2. metadata filtering
3. semantic retrieval
4. personalized ranking
5. natural-language answer generation

The model must not invent viewing history. Answers must be grounded in stored Scenic user data.

---

# 6. Entertainment DNA

Entertainment DNA is Scenic's evolving representation of a user's taste.

It should be richer than a simple "favourite genre" field.

### Possible dimensions

- genres
- subgenres
- themes
- moods
- keywords/tags
- actors
- directors
- studios
- franchises
- languages
- countries
- decades
- runtime preference
- story complexity
- pacing
- intensity
- rating patterns
- completion behavior
- drop behavior
- rewatch behavior
- movie vs series preference
- anime preferences
- weekday/weekend behavior
- time-of-day viewing patterns

### Example presentation

```text
Entertainment DNA

Genre Tendencies
- Sci-Fi: 92%
- Thriller: 87%
- Crime: 78%
- Comedy: 61%

Story Tendencies
- Mystery
- Time travel
- Psychological stories
- Anti-heroes
- Character-driven narratives

Viewing Behavior
- Prefers 90-130 minute movies
- Frequently finishes crime series
- Usually watches series at night
- Rarely completes slow dramas
```

These numbers should be generated from actual user behavior, not arbitrary LLM guesses.

---

# 7. Scenic Match

Scenic Match is a personalized compatibility score between a user and a title.

Example:

```text
93% Scenic Match
```

It is **not** IMDb, Rotten Tomatoes, TMDB rating, or public popularity.

It means:

> "How suitable is this title for this Scenic user?"

### Possible inputs

- Entertainment DNA similarity
- user genre preferences
- theme/tag similarity
- actors/directors affinity
- language
- runtime preference
- ratings on similar titles
- completion history
- watchlist intent
- franchise interest
- negative signals
- recency/context

### Explainability

Every match should be able to produce a short reason, for example:

> Strong match because you frequently finish mystery thrillers, rated *Prisoners* highly, and regularly watch Denis Villeneuve films.

---

# 8. Personalized Recommendation Engine

Recommendation surfaces may include:

- For You
- Because You Watched...
- Similar to Your Favourites
- Hidden Gems for You
- Trending for You
- Watchlist Picks
- Continue This Next
- Upcoming for You
- New Releases for You

### Recommended technical evolution

#### V1
- metadata filtering
- rule-based weighting
- taste vectors
- embeddings
- user feedback signals
- context ranking

#### Later
- collaborative filtering
- user/item embeddings
- learning-to-rank
- behavioral sequence modelling
- user clustering
- more advanced hybrid recommendation models

Scenic does **not** need a custom Netflix-scale ML model for V1.

---

# 9. Smart Watchlist / Smart Queue

The standard watchlist answers:

> "What have I saved?"

The Scenic Smart Queue should answer:

> "What from my watchlist should I actually watch next?"

Possible sections:

- Perfect for Tonight
- Quick Watches
- High Scenic Match
- You've Been Meaning to Watch These
- Continue Before Starting Something New
- Leaving Soon
- Weekend Picks
- Low-Commitment Picks

Possible ranking inputs:

- Scenic Match
- runtime
- current context
- save age
- availability
- release freshness
- user mood
- genre fatigue
- current series commitment
- franchise progress

---

# 10. Natural-Language / Semantic Discovery

Scenic search should support traditional title search and natural-language requests.

Examples:

> "A psychological thriller with a plot twist, after 2015, under two hours."

> "Something like Stranger Things but darker."

> "Funny anime with short episodes."

> "A mystery series I can finish in one weekend."

The AI should parse the request into structured constraints, retrieve real candidates, then rank them.

---

# 11. Spoiler Intelligence

Scenic tracks season/episode progress, so AI must enforce a **spoiler boundary**.

Example:

```text
Breaking Bad
Watched through: Season 3 Episode 6
```

If the user asks:

> "Remind me what is happening in Breaking Bad."

the response must not use information beyond S03E06.

Spoiler intelligence applies to:

- Ask Scenic
- Catch Me Up
- Previously On...
- Character reminders
- Plot explanations
- Series summaries
- title detail assistant
- recommendation explanations when related content may spoil another title

---

# 12. Catch Me Up / Recap

This feature generates a progress-aware, spoiler-safe recap.

Inputs should include:

- title
- season
- last watched episode
- relevant prior episodes
- optional user-selected recap depth

Possible modes:

- 30-second recap
- short recap
- detailed recap
- characters only
- important plot points
- "What do I need to remember?"

---

# 13. Recommendation Explanation Engine

Every important recommendation should be explainable.

Avoid:

> Recommended for you.

Prefer:

> Recommended because you rated *Interstellar* highly, frequently watch science-fiction dramas, and usually prefer movies near two hours.

Possible explanation dimensions:

- taste match
- similar watched titles
- actor/director affinity
- watchlist behavior
- current context
- franchise interest
- runtime fit
- mood fit

The explanation should be generated from known evidence.

---

# 14. Feedback Learning

Scenic should capture explicit and implicit feedback.

| User action | Suggested interpretation |
|---|---|
| Favourite | Very strong positive |
| High rating | Strong positive |
| Rewatch | Very strong positive |
| Finish | Positive/neutral |
| Add to watchlist | Interest |
| Repeated title/detail views | Potential interest |
| Search repeatedly | Interest |
| Skip recommendation | Weak negative |
| Remove from watchlist | Weak negative / cleanup |
| Drop series | Negative |
| Hide title | Strong negative |
| Not interested | Persistent negative |
| Not tonight | Temporary context only |

The AI service should distinguish **persistent preference** from **temporary decision context**.

---

# 15. Smart Continue Watching

Continue Watching should eventually be more intelligent than sorting by last activity.

Useful signals:

- recency
- percentage complete
- episodes remaining
- normal viewing time
- binge behavior
- user affinity
- active vs abandoned status
- season completion opportunity

Example:

> Continue *Breaking Bad* — 4 episodes remain in Season 3.

The system can also separate:

- Active
- Paused
- Probably abandoned
- Completed

---

# 16. AI Smart Lists

Users can create lists using natural language.

Examples:

> "Create a list of 10 psychological thrillers I haven't watched."

> "Make a Marvel catch-up list."

> "Build a weekend anime list."

> "Create a list of 90-minute comedies for family movie night."

The AI must query history and catalogue data rather than generate titles blindly.

---

# 17. Group Recommendation

Future Scenic versions may support multi-user decisions.

Example:

> "What should we watch?"

Inputs:

- selected users
- each user's Entertainment DNA
- common interests
- conflicting dislikes
- watched/unwatched state
- age/content constraints
- runtime
- mood
- availability

The objective is not to select one person's favourite title.

The objective is to find the strongest **combined fit**.

---

# 18. AI Statistics Insights

Scenic statistics are primarily calculated from structured data.

AI should explain patterns rather than invent statistics.

Examples:

- most watched genres
- completion rate
- average rating
- series vs movie ratio
- total seasons/episodes
- most watched actors/directors
- franchise completion
- viewing by month
- runtime totals
- rating tendencies

AI may convert this into insights such as:

> Your thriller viewing increased during the last three months, while comedy dropped compared with the previous quarter.

The actual numbers must come from Scenic analytics.

---

# 19. Year in Review

Year in Review combines verified Scenic statistics with AI narration.

Example:

> 2026 was your year of science fiction. You watched 41 sci-fi titles, almost twice your 2025 total. Your most-watched director was ...

The backend provides the facts. The AI explains and presents them.

---

# 20. Franchise / Universe Intelligence

Franchise/universe tracking is **authoritative backend tracking data first, AI intelligence second**. The Python teammate should consume the hierarchy and progress computed by the main Scenic backend rather than inventing canon, membership or completion.

The full tracking architecture is defined in `FRANCHISE_UNIVERSE_TRACKING.md`. It supports hierarchy (universe/continuity/saga/phase/chapter/franchise), multiple watch orders, title relations, mixed movie/series/anime progress, released-vs-upcoming rules and separate continuities.

Scenic should understand structured collections such as:

- Marvel Cinematic Universe
- DC universes
- Star Wars
- Harry Potter / Wizarding World
- Lord of the Rings
- major anime franchises
- other film/TV universes

Questions may include:

> "How much of the MCU have I completed?"

> "What should I watch next in release order?"

> "Which Star Wars titles haven't I watched?"

This requires franchise metadata + user tracking, with AI providing interpretation and conversational access.

---


# 20A. Taste Evolution

Entertainment DNA is a current-state profile. **Taste Evolution** explains how that profile changes over time.

Examples:

- genre interest by year or semester
- growing/declining interest in themes
- runtime tolerance changes
- changing language/country preferences
- movie vs series vs anime shifts
- director/actor affinity changes
- completion/drop behavior changes
- changes in preferred intensity, pacing, or complexity

Example insight:

> Your interest in psychological and mystery stories has increased over the last two years, while your completion rate for long fantasy series has fallen.

The underlying statistics must come from Scenic data. AI may summarize the trend but must not invent it.

---

# 20B. Hidden Gem Detector

Hidden Gems should be a **dedicated recommendation mode**, not just a Home row label.

Goal:

> Find titles that strongly match the user but are less likely to appear in mainstream popularity-first discovery.

Possible factors:

- high Scenic Match
- strong metadata similarity
- sufficient rating/review quality
- lower popularity/exposure
- not already watched
- not repeatedly dismissed
- diversity relative to recent viewing

The implementation should avoid a single universal definition of "hidden gem." Popularity thresholds may vary by country, media type, age, and catalogue size.

---

# 20C. Comfort Zone Breaker / Exploration Mode

This mode intentionally increases novelty while keeping a meaningful connection to the user's taste.

Example:

> A user who mostly watches Japanese psychological anime may be offered a Korean psychological thriller because the themes and tone match even though the medium/country differs.

This requires a controllable **exploration vs familiarity** parameter.

Possible modes:

- Safe Pick
- Familiar but New
- Explore
- Escape My Comfort Zone
- Surprise Me

The engine should never interpret exploration as permission to ignore explicit dislikes or hard constraints.

---

# 20D. Smart Watch Planner

The Decision Engine normally returns a small set of next actions.

The **Smart Watch Planner** can plan an entire viewing window.

Examples:

> "I have 45 minutes."

Possible result:
- 1 x 42-minute episode

> "I have 3 hours tonight."

Possible result:
- finish 2 remaining episodes of an active mini-series
- or one 110-minute movie + one 45-minute episode

> "Plan my weekend."

Possible result:
- a realistic multi-title plan using total runtime, current progress, preferences, and release urgency

Planner inputs may include:

- total available time
- breaks
- current progress
- episode runtimes
- movie runtimes
- whether starting new content is allowed
- mood
- company
- user goals
- priority titles
- availability

The planner should prefer realistic plans and avoid filling every available minute just because it can.

---

# 20E. Commitment Intelligence

For series and anime, genre similarity alone is not enough.

Scenic should understand:

- episodes remaining
- seasons remaining
- estimated hours remaining
- average episode runtime
- whether the user is near a season finale
- whether a new season is approaching
- whether the title has been stalled
- whether the series is ongoing or ended
- whether the user usually completes similar commitments

Examples:

> 2 episodes / ~96 minutes remain in this season.

> A new season starts in 18 days and you have 7 episodes left.

> You usually drop series longer than five seasons, so this is a higher-commitment recommendation.

Commitment signals should influence the Decision Engine, Smart Queue, Continue Watching, and Watch Planner.

---

# 20F. Recommendation Refinement, Memory and Confidence

Recommendations should be interactive rather than one-shot.

## Refinement controls

A recommendation result should support actions such as:

- shorter
- longer
- lighter
- darker
- funnier
- more serious
- more obscure
- more familiar
- less commitment
- only from my watchlist
- continue something
- start something new
- not tonight
- not interested
- never recommend this

These controls should update the **current decision session** without accidentally rewriting the user's permanent taste unless the user explicitly chooses a persistent action.

## Recommendation memory

Scenic should remember:

- what was recommended
- when it was recommended
- why it was recommended
- which context was active
- whether it was opened
- saved
- started
- completed
- skipped
- rejected
- marked not tonight
- marked not interested

This helps prevent repetitive recommendations and enables evaluation.

## Confidence

Where useful, return:

- ranking confidence
- reason strength
- metadata completeness
- availability freshness
- cold-start / low-data status

Do not show fake precision. A 94% Scenic Match should only be displayed if the product has a defined scoring interpretation.

---

# 20G. Taste Correction and "Why Scenic Thinks This"

Entertainment DNA must be correctable.

Users should be able to say:

- "I don't actually like this genre."
- "I watched these because my family chose them."
- "Stop treating this actor as a preference."
- "I like horror, just not tonight."
- "This rating was for nostalgia, not because I want similar recommendations."

A **Why Scenic thinks this** panel can show the evidence behind an inferred preference.

Example:

```text
Scenic thinks you like psychological thrillers because:
- 11 completed titles
- 8.6 average rating
- 3 rewatches
- low drop rate
```

Corrections should become high-quality labels for the taste model.

---

# 20H. Availability, Subscription and Release Intelligence

Availability should be more than a "Where to Watch" link.

## Availability-aware decisioning

Decision constraints may include:

- only services the user has
- subscription only
- free options allowed
- rental allowed
- purchase allowed
- country/region
- currently available
- leaving soon

Availability data must include source/region/freshness when possible.

## Watchlist coverage

Examples:

> 11 titles from your watchlist are currently on Service A.

> 6 high-priority titles are available on Service B this month.

## Subscription intelligence

If the product later allows users to enter service costs, Scenic can estimate:

- watched hours per service
- completed titles per service
- backlog coverage
- unused-service warnings
- possible pause suggestions
- useful resubscribe windows

This is a later intelligence feature, not an MVP requirement.

## Release urgency

Ranking may consider:

- title leaving a service soon
- new season approaching
- finale approaching
- followed movie release
- watchlist title becoming available
- long-stalled title
- unfinished backlog before sequel/release

---

# 20I. Social Compatibility and Group Intelligence

Group Recommendation is only one part of the social intelligence layer.

## Two-user compatibility

Scenic may calculate compatibility using:

- shared watched titles
- rating agreement
- genre/theme overlap
- director/actor/studio affinity
- shared dislikes
- completion patterns
- language/runtime preferences

A compatibility percentage should only be shown if the scoring method is documented.

## Group Watch Planner

For multiple users, the system may:

1. build each person's candidate eligibility
2. remove titles already watched by everyone when appropriate
3. penalize strong dislikes
4. calculate group-fit scores
5. preserve fairness so one person's profile does not dominate
6. return a shortlist
7. optionally allow group voting

## Spoiler-safe group progress

When generating recaps, discussion helpers, or character explanations for a group, use the safest shared spoiler boundary—normally the least-advanced participating member unless the group explicitly chooses otherwise.

---

# 20J. Goal-Aware Intelligence

AI can help users act on explicit goals.

Examples:

- finish a season this week
- catch up before a new season
- complete the MCU
- reduce a stale watchlist
- watch five films from a specific country
- finish a mini-series over the weekend

Goal-aware recommendations should use real progress and available time.

Achievements and streaks are normal product/gamification features; the AI developer only needs them when they become an input to planning or personalized guidance.

---

# 20K. Search Intelligence Beyond Embeddings

Semantic search is only one part of a strong search experience.

The surrounding Scenic search system should support:

- title aliases
- translated/original titles
- typo tolerance
- prefix/fuzzy matching
- actors/directors/people
- studios
- franchises/collections
- recent searches
- persistent filters
- hide watched
- hide dropped
- language filters
- runtime filters
- never-show exclusions

The Python AI service may parse natural-language constraints, but basic catalogue search quality belongs primarily to the main backend/search layer.

---

# 20L. Additional AI-Related Analytics

The broader tracking system can provide useful signals to AI:

- movie / series / season / episode counts
- genre/theme/country/language/decade distributions
- actor/director/studio filmography progress
- rewatches
- completion rate
- drop rate
- binge patterns
- watching calendar / heatmap
- backlog age
- remaining runtime
- franchise/phase/saga progress
- recommendation acceptance history
- exploration rate
- group taste overlap
- notes/tags where the user intentionally makes them available

These are primarily structured analytics. AI should use or explain them rather than fabricate them.

---

# 20M. AI Product Metrics

The team should evaluate AI by whether it reduces decision friction and improves useful outcomes.

Suggested metrics:

- **Decision success rate:** percentage of Tonight sessions ending in a selected/started title
- **Time to decision:** median time from entering the decision flow to choosing
- **Recommendation acceptance:** starts, saves, or positive feedback from ranked picks
- **Repeat-recommendation rate:** how often already-rejected titles reappear incorrectly
- **Queue health:** stale-backlog reduction and percentage of items with actionable priority
- **Taste correction rate:** frequency of user corrections to inferred preferences
- **Spoiler violation rate:** must be zero in validated cases
- **Cold-start usefulness:** reviewer/user acceptance before enough behavioral history exists
- **Recommendation diversity:** avoid collapsing to the same genres/titles
- **AI cost per active user:** track model/embedding cost as the system grows

Do not optimize only for time spent inside Scenic. A good decision product may succeed by helping the user leave the app quickly and start watching.

---

# 20N. Full AI Intent Catalogue for Ask Scenic

The earlier intent list is only the MVP. The full bot may eventually support:

```text
WATCH_RECOMMENDATION
WATCH_PLAN
REFINE_RECOMMENDATION
SURPRISE_ME
FIND_TITLE
SEMANTIC_DISCOVERY
HISTORY_QUERY
MEMORY_RECALL
TASTE_QUERY
TASTE_EVOLUTION_QUERY
TASTE_CORRECTION
WATCHLIST_QUERY
SMART_QUEUE_QUERY
CONTINUE_QUERY
PROGRESS_QUERY
REMAINING_TIME_QUERY
FRANCHISE_QUERY
FILMOGRAPHY_QUERY
RELEASE_QUERY
AVAILABILITY_QUERY
SUBSCRIPTION_QUERY
EXPLANATION_QUERY
RECAP_QUERY
CHARACTER_REMINDER
LIST_GENERATION
GROUP_RECOMMENDATION
COMPATIBILITY_QUERY
STATS_QUERY
YEAR_REVIEW_QUERY
GOAL_PLAN
```

Every intent should map to a validated Scenic capability. Unknown intents should not cause the LLM to invent unsupported actions.

---

# 21. Scenic Pages Related to AI

## Dedicated AI-first pages

These should be treated as first-class AI product surfaces:

1. **Tonight / Decision**
   - Main Decision Engine UI
   - mood
   - available time
   - media type
   - company
   - commitment
   - intensity
   - AI recommendation cards

2. **Ask Scenic**
   - full conversational assistant
   - account-aware requests
   - recommendation requests
   - memory queries
   - lists/actions
   - explanations

3. **Entertainment DNA**
   - taste profile
   - preference visualization
   - genre/theme/person affinity
   - behavioral patterns
   - user corrections

4. **Entertainment Memory**
   - natural-language history search
   - remembered title discovery
   - viewing-history questions

5. **Smart Watchlist**
   - ranked watchlist
   - personalized sections
   - current-context prioritization

6. **Taste Evolution**
   - preference changes over time
   - explainable trend summaries
   - correction controls

7. **Smart Watch Planner**
   - plan 45 minutes / one evening / a weekend
   - combine multiple episodes or titles
   - consider current progress and commitments

8. **Compatibility / Group Decision**
   - two-user taste compatibility
   - multi-user candidate ranking
   - optional group voting

9. **Availability Intelligence** *(later phase)*
   - personalized provider coverage
   - availability urgency
   - optional subscription-value insights

## Other pages that consume AI

| Scenic page | AI usage |
|---|---|
| Home | Personalized sections and Decision Engine entry |
| Discover | Recommendation ranking |
| Search | Semantic / natural-language search |
| Movie Detail | Scenic Match, explanations, similar-for-you |
| Series Detail | Match, progress intelligence, recap |
| Anime Detail | Match, progress intelligence, recommendation |
| Watchlist | Smart Queue |
| Library | Personalized organization/filtering |
| Continue Watching | Smart ranking |
| History | Source for Memory and DNA |
| Statistics | AI-generated insights from real stats |
| Year in Review | AI narrative |
| Lists | AI list generation |
| Upcoming / Releases | Personalized upcoming titles |
| Franchise / Universe | Completion and next-title intelligence |
| Friends / Group Decision | Group recommendation |
| Notifications | Personalized release/recommendation alerts |
| Settings / AI Preferences | User corrections and recommendation controls |
| Calendar | AI can prioritize releases and catch-up urgency |
| Provider / Streaming Availability | Availability-aware ranking and coverage |
| Taste Evolution | Historical preference changes |
| Compatibility | Two-user taste comparison |
| Group Planner | Group shortlist and consensus |
| Goals | Goal-aware planning and catch-up recommendations |
| People / Filmography | Personalized actor/director/studio progress queries |

---

# 22. Suggested AI Sections on Home

The Scenic home page should feel like a personal entertainment command center.

Possible sections:

1. Continue Watching
2. What Should I Watch Tonight?
3. For You
4. Because You Watched...
5. Watchlist Picks
6. Trending for You
7. Hidden Gems for You
8. Entertainment DNA Snapshot
9. Upcoming for You
10. Recently Watched

The Decision Engine entry can be a prominent card:

```text
Not sure what to watch?
Tell Scenic your mood and how much time you have.

[ Ask Scenic ]
```

---

# 23. System Ownership

The **Node.js / TypeScript Scenic backend remains the primary application backend**.

The Python AI service should be an **intelligence service**, not a duplicate application backend.

## Python Intelligence Service owns

- recommendation scoring
- candidate ranking
- Decision Engine logic
- Entertainment DNA calculation
- taste modelling
- semantic similarity
- embeddings
- context ranking
- Scenic Match
- natural-language query interpretation
- recommendation explanation data
- Entertainment Memory reasoning
- group recommendation logic
- future ML models

## Main Scenic Backend owns

- authentication
- users
- authorization
- movies / series / anime records
- external metadata synchronization
- watch history persistence
- watchlist persistence
- ratings
- favourites
- episode/season progress
- lists
- social/friend data
- franchise metadata
- availability data
- database ownership
- CRUD
- public application APIs
- AI service authentication / access control

---

# 24. Recommended Architecture

```text
React Frontend
      |
      v
Node.js / TypeScript / Express Scenic API
      |
      +-----------------------------+
      | Auth / Users                |
      | Catalogue                   |
      | Tracking                    |
      | Watchlist                   |
      | Ratings / Favourites        |
      | Progress                    |
      | Lists                       |
      | Franchise Data              |
      | Availability                |
      +-----------------------------+
      |
      v
Python Intelligence Service
      |
      +-----------------------------+
      | Decision Engine             |
      | Recommendation Engine       |
      | Entertainment DNA           |
      | Scenic Match                |
      | Semantic Search             |
      | Embeddings                  |
      | Context Ranking             |
      | Entertainment Memory        |
      | Explanation Engine          |
      +-----------------------------+
```

### Important integration rule

The frontend should normally call the **main Scenic API**, not the Python service directly.

This keeps:

- authentication centralized
- user data controlled
- APIs consistent
- the AI service replaceable
- service boundaries clean

---

# 25. AI Request Pipeline

Avoid sending all user data directly to an LLM and asking it to choose a title.

A better pipeline:

```text
User Request
    |
    v
Intent + Constraint Parser
    |
    v
Candidate Retrieval
    |
    v
Hard Filters
    |
    v
Taste / Scenic Match Scoring
    |
    v
Context Ranking
    |
    v
Diversification
    |
    v
Final Candidates
    |
    v
Explanation / Conversational Layer
    |
    v
Scenic Response
```

The LLM is especially useful for:

- parsing ambiguous natural language
- extracting intent
- extracting constraints
- semantic interpretation
- conversational response
- evidence-based explanation

The LLM should **not** be the catalogue database.

---

# 26. Data the Intelligence Service May Need

Conceptually, the main backend may provide:

```text
User
 |
 +-- Profile
 +-- Watch History
 +-- Ratings
 +-- Favourites
 +-- Watchlist
 +-- Episode / Season Progress
 +-- Completed Titles
 +-- Dropped Titles
 +-- Rewatches
 +-- Lists
 +-- Recommendation Feedback
 +-- Persistent Preferences
 +-- Current Decision Context
 +-- Franchise Progress
 +-- Availability Context
 +-- Candidate Title Metadata
```

The exact payload should be minimized for each AI task rather than sending the entire account every time.

---

# 27. Possible Internal API Surface

These are architectural examples, not final contracts.

```text
POST /ai/decision
POST /ai/recommendations
POST /ai/scenic-match
POST /ai/semantic-search
POST /ai/query/parse
POST /ai/memory/search
GET  /ai/dna/:userId
POST /ai/dna/recalculate
POST /ai/watchlist/rank
POST /ai/continue-watching/rank
POST /ai/explain
POST /ai/group-recommendation
POST /ai/compatibility
POST /ai/lists/generate
POST /ai/watch-plan
POST /ai/recommendations/refine
POST /ai/taste/correct
POST /ai/taste/evolution
POST /ai/availability/rank
POST /ai/goals/plan
```

Prefer service-to-service authentication.

Do not expose internal AI endpoints publicly unless there is a specific reason.

---

# 28. Suggested Decision Request Contract

Example:

```json
{
  "user_id": "user_123",
  "context": {
    "available_minutes": 120,
    "media_types": ["movie"],
    "moods": ["funny", "light"],
    "company": "alone",
    "commitment": "single_sitting",
    "intensity": "low"
  },
  "preferences": {
    "exclude_watched": true,
    "exclude_dropped": true,
    "temporary_exclusions": ["horror"]
  },
  "candidate_ids": [
    "movie_1",
    "movie_2",
    "movie_3"
  ]
}
```

Example response:

```json
{
  "recommendations": [
    {
      "title_id": "movie_2",
      "scenic_match": 0.94,
      "rank": 1,
      "reason_codes": [
        "genre_affinity",
        "runtime_fit",
        "mood_fit",
        "similar_high_rating"
      ],
      "explanation": "A strong fit for tonight because..."
    }
  ]
}
```

---

# 29. Reason Codes

Do not rely only on generated explanation text.

The recommendation service should ideally return machine-readable reasons.

Examples:

```text
genre_affinity
theme_affinity
actor_affinity
director_affinity
franchise_interest
runtime_fit
mood_fit
company_fit
availability_fit
watchlist_interest
similar_high_rating
rewatch_pattern
recent_search_interest
completion_likelihood
trending_with_taste
new_release_with_taste
```

This helps the frontend display consistent explanations and makes AI behavior testable.

---

# 30. Recommendation Quality Rules

The engine should avoid:

- titles already watched when the user wants new content
- titles explicitly hidden
- dropped titles unless the user asks to reconsider them
- repeated recommendations with no reason
- incompatible runtime
- spoilers
- unavailable titles when availability is a hard constraint
- over-recommending only the user's top genre
- treating popularity as personalization
- presenting an LLM hallucination as catalogue data

The engine should support **diversity** so all 3 recommendations are not nearly identical.

---

# 31. AI V1 Scope

A realistic first implementation should prioritize:

### P0 — Foundation

- shared AI request/response schemas
- user taste feature calculation
- recommendation feedback model
- basic candidate scoring
- basic Scenic Match
- reason codes
- tests

### P1 — Decision Engine

- context parser
- hard constraints
- scoring
- top 3 decisions
- explanations
- Decision page integration

### P2 — Entertainment DNA

- genre/theme/person preferences
- rating signals
- completion/drop/rewatch signals
- DNA API
- DNA page integration

### P3 — Ask Scenic

Initial intents:

- WATCH_RECOMMENDATION
- FIND_TITLE
- HISTORY_QUERY
- TASTE_QUERY
- WATCHLIST_QUERY
- FRANCHISE_QUERY
- EXPLANATION_QUERY
- LIST_GENERATION

### P4 — Semantic Discovery

- title/content embeddings
- natural-language query embeddings
- semantic candidate retrieval
- personalization reranking

### P5 — Memory + Spoiler Intelligence

- history retrieval
- remembered-title search
- progress-aware context
- spoiler boundary enforcement
- recap

---

# 32. Suggested Implementation Strategy

For V1, use a **hybrid intelligence approach**:

```text
Structured metadata
+ deterministic filters
+ weighted ranking
+ user taste vectors
+ embeddings
+ explicit feedback
+ LLM parsing/explanations
```

Do not start by training a large custom model.

The architecture should allow more advanced ML to replace or augment scoring later.

---

# 33. Testing Requirements

AI output should be tested like application logic.

Important test categories:

- watched content excluded correctly
- runtime constraints respected
- media-type constraints respected
- hidden content excluded
- dropped-title behavior correct
- "not tonight" does not become permanent dislike
- high-rated similar content increases match
- negative signals reduce match
- recommendation diversity
- stable scoring for identical input
- explanation reason codes match scoring evidence
- spoiler boundary never exceeded
- malformed LLM parse handled safely
- missing profile/history handled gracefully
- cold-start users receive sensible recommendations
- repeated rejected recommendations are suppressed appropriately
- recommendation-session refinements do not incorrectly alter permanent taste
- taste corrections affect later recommendations
- commitment estimates use correct remaining episode/runtime data
- recommendation confidence is not emitted when unsupported
- availability region/freshness is respected
- group ranking does not allow one user to dominate unfairly
- group spoiler boundary uses the least-advanced participant by default
- hidden-gem mode preserves quality and taste fit while increasing novelty
- comfort-zone mode increases exploration without violating hard dislikes

---

# 34. Cold Start

New users will have little or no watch history.

Possible onboarding inputs:

- favourite titles
- favourite genres
- disliked genres
- favourite actors/directors
- movie vs series preference
- preferred languages
- anime interest
- sample title comparisons

Cold-start recommendations can initially combine:

- onboarding choices
- quality/popularity
- diversity
- contextual request

As user history grows, behavior should outweigh onboarding answers.

---

# 35. Privacy / Safety Principles

The intelligence service should:

- request only data required for the task
- avoid logging unnecessary personal user data
- avoid leaking one user's taste/history to another user
- use service authentication
- respect deleted history and preferences
- avoid exposing raw internal model prompts
- distinguish generated explanation from factual catalogue data

---

# 36. Success Criteria

The AI system is successful when users feel that Scenic:

1. remembers what they watched
2. understands what they like
3. understands what they want **right now**
4. helps them choose quickly
5. does not repeatedly recommend irrelevant content
6. can explain its recommendations
7. respects their watch progress and avoids spoilers
8. gets more useful as they use Scenic

---

# 37. One-Sentence Product Definition for the AI Developer

> **Scenic AI is a personal entertainment intelligence system that remembers what the user watches, builds an evolving model of their taste, understands their current situation, and uses that information to help them discover, recall, understand, and decide what to watch next—with Ask Scenic acting as the natural-language interface to that intelligence.**

---

# 38. The Three Concepts to Remember

```text
MEMORY
  |
  v
TASTE
  |
  v
DECISION
```

If an AI feature does not improve at least one of these three concepts, question whether it belongs in the core Scenic intelligence system.

---

## Related Scenic Documentation

This document provides the complete AI handoff view. It should be read together with:

- `docs/DECISION_ENGINE.md`
- `docs/FRANCHISE_UNIVERSE_TRACKING.md`
- `docs/ARCHITECTURE.md`
- `docs/API.md`
- `docs/DATA_MODEL.md`
- `docs/REQUIREMENTS.md`
- `PROJECT.md`
- `PLAN.md`

---

**Document status:** Scenic 2.0 full AI architecture, feature inventory, and teammate handoff  
**Deep audit:** reconciled against earlier CineTrack/Scenic plans, Scenic product research, and the current Scenic 2.0 repository.  
**Scope note:** this document records the **full product intelligence vision**. It does not mean every item belongs in the academic MVP; use PROJECT.md / REQUIREMENTS.md / PLAN.md for committed delivery scope.  
**Last updated:** 2026-09-29
