# Project charter — Scenic 2.0

## Problem
People keep fragmented watchlists, lose track of series progress, and spend time choosing a movie despite having many options. Scenic brings discovery, tracking, and a short, explainable recommendation list into one application.

## Users and value
Primary users are individual movie and series viewers. A viewer should be able to find a title, save it, record progress, and understand why another title is suggested.

## Objectives and measurable acceptance
1. A new user can register, sign in, search, save a title, and mark it watched in a complete demonstration.
2. A series viewer can record episodes and see accurate season and series progress after refreshing.
3. A dashboard agrees with known seeded viewing records.
4. A user receives up to ten eligible recommendations with understandable reasons.
5. User A cannot read or modify User B's private records.
6. Core tracking remains usable when the decision service is unavailable.

## Scope
**Core release:** authentication; metadata search/details; watchlist; movie completion; episode progress; dashboard; baseline recommendations; responsive accessible interfaces; reproducible setup; tests and deployment documentation.

**After core acceptance:** curated Marvel/other franchise collections, ratings and recommendation feedback, data export, richer filters.

**Excluded initially:** video streaming, piracy links, payments, social feeds/chat, advanced collaborative ML, native mobile clients, automatic streaming-provider availability, offline synchronization.

## Deliverables
Source code; reviewed requirements; architecture and schema; API contracts; test evidence; working deployment if budget permits; reproducible local demo; group contribution log; presentation and demonstration.

## Proposed technical baseline
React/TypeScript frontend, Node.js/TypeScript/Express API, Prisma/PostgreSQL persistence, Python/FastAPI recommendation service. These reflect the initial project direction; confirm with the lecturer and group before scaffolding.

## Assumptions needing confirmation
- An eight-week plan is an estimate; academic deadline is unknown.
- Team roles may be combined or shared depending on group size.
- Metadata provider, authentication approach, runtime versions, hosting and budget are undecided.
- No application code or test results exist in this repository at initialization.

## Success and change control
Core acceptance criteria take priority over optional features. Record scope changes in docs/DECISIONS.md with impact on effort, dependencies and delivery. A feature is complete only when implemented, reviewed, tested and documented.
