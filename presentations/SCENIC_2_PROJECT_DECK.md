# Scenic 2.0 — project presentation deck

Use this as the canonical slide-by-slide source for the group proposal and later final presentation.

## Slide 1 — Scenic 2.0

**Everything you watch. One intelligent place.**

Movie • TV Series • Anime

Subtitle: Tracking + Entertainment Intelligence

Visual: premium dark cinematic composition using actual Scenic branding/UI artwork when available.

Speaker point: Scenic is not a streaming service; it is the layer that remembers, organizes and helps users choose.

---

## Slide 2 — The problem

Three concrete pains:
- “What episode was I on?”
- “Where did I save that movie?”
- “I have a huge watchlist — what should I actually watch tonight?”

Visual: three simple problem cards, not generic AI graphics.

---

## Slide 3 — The product model

Large center flow:

**MEMORY → TASTE → DECISION**

Memory: history, progress, watchlist, ratings.
Taste: Entertainment DNA and preference signals.
Decision: Watch Next, Smart Queue and recommendations.

---

## Slide 4 — Core journey

Discover → Save → Watch → Track → Analyze → Decide.

Show six small real/mocked Scenic frames connected as one user journey.

---

## Slide 5 — Main Scenic pages

Show a clean sitemap or UI strip:
- Home
- Discover
- Search
- Media Details
- Library
- Watchlist
- Continue Watching
- History
- Statistics
- Entertainment DNA
- Watch Next
- Settings

Optional/future: Year in Review, Calendar, Franchise Progress, Ask Scenic, Group Decision.

---

## Slide 6 — Home: personal command center

Mockup focus:
- Continue Watching
- Up Next
- For You
- Watchlist picks
- Compact weekly stats
- Upcoming releases

Message: logged-in Home should help the user continue or decide, not repeat marketing copy.

---

## Slide 7 — Tracking that understands series

Visual: series page showing seasons/episodes and progress.

Explain:
- episode-level state;
- season completion;
- series completion;
- Continue Watching;
- refresh-safe persistence;
- rewatches later.

---

## Slide 8 — Library and statistics

Library statuses:
Watching • Completed • Plan to Watch • Paused • Dropped • Favorites.

Statistics examples:
- movies/series/seasons/episodes;
- genre distribution;
- progress;
- later watch time, heatmaps and Year in Review.

---

## Slide 9 — Franchise & universe tracking

Examples: Marvel, DC, Star Wars and anime franchises.

Show:
- hierarchy such as Universe → Saga/Chapter → Phase/Arc → Title;
- separate continuities where required;
- released titles completed vs upcoming items;
- movie/series/anime breakdown;
- episode progress for member series;
- estimated remaining runtime;
- release, chronological and curated watch orders;
- the next unwatched item.

Important: a mixed-media universe should not show an unexplained percentage. State whether progress is measured by released required titles, eligible episodes or estimated runtime.

Make clear this is staged after core tracking unless already implemented.

---

## Slide 10 — Watch Next / Decision Engine

Input examples:
- time available;
- mood;
- watching alone/with others;
- commitment length;
- continue vs new;
- availability and urgency.

Output:
1–5 ranked choices with short explanations.

Key principle: decision support, not an endless poster wall.

---

## Slide 11 — Scenic intelligence roadmap

MVP:
- deterministic candidate filtering;
- weighted ranking;
- explanations;
- cold-start/fallback handling.

Next:
- Entertainment DNA;
- Scenic Match;
- Smart Queue;
- Hidden Gems;
- recommendation feedback.

Future:
- Ask Scenic;
- semantic discovery;
- spoiler-safe recaps;
- group recommendations;
- ML only after data/evaluation exists.

---

## Slide 12 — Architecture

Diagram:

User
↓
React + TypeScript
↓
Express + TypeScript API
├─ PostgreSQL + Prisma
├─ Metadata provider adapters
└─ Python/FastAPI Decision Service

Explain:
- API owns authentication/authorization and source-of-truth data.
- Python owns recommendation/decision algorithms.
- browser never connects to the database/private service directly.

---

## Slide 13 — Group development workflow

Flow:

Issue → feature branch → PR → review → develop → milestone release → main.

Show workstreams:
- Frontend/UX
- Backend/data
- Decision/AI
- QA/testing
- Integration/documentation

Replace roles with actual member names before presenting.

---

## Slide 14 — Delivery roadmap

Week 1: agree scope/contracts.
Week 2: scaffold/auth/database.
Week 3: first complete movie flow.
Week 4: series progress + stats.
Week 5: decision baseline.
Week 6: integration/accessibility.
Week 7: security/testing/deployment.
Week 8: final demo/report/presentation.

If the real deadline differs, update this slide rather than pretending the eight-week plan is fixed.

---

## Slide 15 — Quality and trust

- cross-user authorization;
- no secrets in repository;
- idempotent watch events;
- exact fixture-based statistics;
- loading/empty/error states;
- graceful AI/provider outage;
- spoiler boundaries;
- accessible responsive UI;
- reproducible setup and tests.

---

## Slide 16 — MVP vs vision

Two columns.

**MVP**
Auth, search/details, watchlist/library, movie completion, episode progress, Continue Watching, dashboard, deterministic recommendations, tests.

**Product vision**
DNA, Smart Queue, first-class franchise/universe tracking and watch orders, Wrapped, availability intelligence, Ask Scenic, spoiler-safe intelligence, group decisions.

Message: we protect the vision without over-scoping the first release.

---

## Slide 17 — Demo plan

Final presentation sequence:
1. Sign in.
2. Search a title.
3. Add to watchlist.
4. Mark a movie watched.
5. Track an episode.
6. Show Continue Watching.
7. Show changed statistics.
8. Request a recommendation.
9. Explain the reason returned.

Use synthetic demo accounts/data.

---

## Slide 18 — Closing

**Scenic remembers what you watch, understands your taste, and helps you decide what comes next.**

Show repository/team/course information.

Do not add unsupported claims, fake user numbers or fake accuracy metrics.
