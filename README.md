# Scenic 2.0

A group project for discovering movies and series, tracking viewing progress, and choosing what to watch next.

**Status:** Planning and documentation. Application code, infrastructure, and automated checks have not been implemented.

## Product scope
- Discover movies and television series.
- Maintain a personal watchlist and watched history.
- Track series at episode and season level.
- View movie, series, season, and genre statistics.
- Receive explainable suggestions through a Python decision engine.
- Track progress through curated collections, including a proposed Marvel collection.

Scenic stores metadata and personal viewing records; it does not host or stream videos.

## Planned architecture
React + TypeScript → Express + TypeScript → PostgreSQL via Prisma.
The Express API calls a separate Python/FastAPI decision service. The browser never connects directly to the database or private decision service.

## Start here
1. Read [PROJECT.md](PROJECT.md) for scope and success criteria.
2. Follow [PLAN.md](PLAN.md) for milestones and the first working increment.
3. Assign responsibilities using [Team workflow](docs/TEAM.md).
4. Agree on [Requirements](docs/REQUIREMENTS.md), [Data model](docs/DATA_MODEL.md), and [API design](docs/API.md).
5. Follow [Setup](docs/SETUP.md) when scaffolding begins.
6. Use [CONTRIBUTING.md](CONTRIBUTING.md) for every change.

## Documentation
| Document | Purpose |
|---|---|
| [Project charter](PROJECT.md) | Problem, scope, deliverables, assumptions |
| [Implementation plan](PLAN.md) | Proposed eight-week sequence and exit criteria |
| [Requirements](docs/REQUIREMENTS.md) | Features, acceptance criteria, quality targets |
| [Architecture](docs/ARCHITECTURE.md) | Service boundaries and failure handling |
| [Data model](docs/DATA_MODEL.md) | Entities, constraints, statistics definitions |
| [API design](docs/API.md) | Proposed contracts and error behavior |
| [Decision engine](docs/DECISION_ENGINE.md) | Academic MVP baseline algorithm and evaluation |
| [AI system handoff](docs/AI_SYSTEM_HANDOFF.md) | Full Scenic intelligence vision, AI features, pages, service ownership and roadmap |
| [Setup](docs/SETUP.md) | Scaffolding and onboarding steps |
| [Team workflow](docs/TEAM.md) | Ownership, review, meetings, contribution evidence |
| [Backlog](docs/BACKLOG.md) | Tasks, dependencies, completion criteria |
| [Testing](docs/TESTING.md) | Test matrix and release gates |
| [Delivery](docs/DELIVERY.md) | Deployment, rollback, demonstration |
| [Risks and decisions](docs/DECISIONS.md) | Open questions and architecture decisions |
| [Presentation](docs/PRESENTATION.md) | Proposal and final demonstration outline |
| [Meeting template](docs/MEETING_TEMPLATE.md) | Decisions, actions, blockers |
| [Security](SECURITY.md) | Credential handling and vulnerability reporting |

## Team
Member names, team size, course requirements, submission date, and deployment budget are **TBD**. Role slots and milestone weeks are planning suggestions, not confirmed commitments.

## License
No software license has been selected. Agree on licensing as a team before adding a license or redistributing third-party assets.
