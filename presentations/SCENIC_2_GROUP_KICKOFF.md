# Scenic 2.0 — Group project kickoff presentation

A concise team-facing presentation for the first project meeting. Use the longer `SCENIC_2_PROJECT_DECK.md` for proposal/final presentation work.

## Slide 1 — Scenic 2.0

**Everything you watch. One intelligent place.**

Movies • TV Series • Anime

Group project kickoff

---

## Slide 2 — What Scenic is

Scenic is a tracking + entertainment-intelligence platform.

It helps users:
- remember what they watched;
- track movie/series/anime progress;
- organize watchlists;
- understand viewing patterns;
- decide what to watch next.

It is **not** a streaming service.

---

## Slide 3 — Product model

**MEMORY → TASTE → DECISION**

Memory: history, progress, watchlist, ratings.

Taste: genre/person/franchise preferences and Entertainment DNA.

Decision: recommendations, Smart Queue, Watch Next and future Ask Scenic.

---

## Slide 4 — MVP boundary

The first assessed release focuses on:
- authentication;
- search/details;
- watchlist/library;
- movie completion;
- episode progress;
- Continue Watching;
- dashboard statistics;
- deterministic recommendations;
- testing and reproducible setup.

P1/P2 features must not delay this baseline.

---

## Slide 5 — Architecture

React + TypeScript

↓ Main application API

Node.js + TypeScript + Express

├─ PostgreSQL + Prisma  
├─ metadata provider adapter  
└─ Python + FastAPI decision service

The main API owns authentication and source-of-truth data. Python owns intelligence/ranking logic.

---

## Slide 6 — First vertical slice

**Sign in → Search → Details → Watchlist → Watched → Dashboard**

Goal: prove frontend + API + database + auth + statistics work together before expanding scope.

---

## Slide 7 — Group workstreams

- Frontend / UX
- Backend / Data
- Tracking Core
- AI / Decision Engine
- QA / Testing
- CI / Delivery
- Documentation / Presentation
- Optional Franchise / Universe Tracking

Replace workstreams with real owner + reviewer names after kickoff.

---

## Slide 8 — Git workflow

Issue → short-lived branch → PR → review → `develop` → release PR → `main`

`main` = stable demonstration branch  
`develop` = integration branch

No direct unfinished work to `main`.

---

## Slide 9 — Delivery sequence

1. contracts + provider + schema;
2. foundations/auth/database;
3. first movie flow;
4. series progress + stats;
5. recommendation baseline;
6. integration/accessibility;
7. stabilization/security/deployment;
8. final demo/report/presentation.

---

## Slide 10 — Quality rules

- cross-user authorization;
- no secrets in repo;
- repeatable migrations;
- exact fixture-based statistics;
- graceful provider/AI failure;
- responsive/accessibility states;
- test evidence;
- synthetic demo data.

---

## Slide 11 — Main project risk

The biggest risk is **over-scoping before the first complete flow works**.

Rule: P1/P2 work starts only when unresolved P0 work is under control.

---

## Slide 12 — Kickoff decisions required

Before coding:
- team roster;
- owner/reviewer per workstream;
- deadline/rubric;
- metadata provider;
- runtime versions;
- auth/session approach;
- first schema/API contracts;
- Sprint 1 issue assignments.

---

## Slide 13 — First team target

At the next integration checkpoint, every member should be able to run the project and demonstrate the first vertical slice or their directly supporting component.

**Build together. Integrate early. Keep `main` demonstrable.**
