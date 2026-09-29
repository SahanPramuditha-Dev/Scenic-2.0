# Scenic 2.0

Scenic 2.0 is a group project for building a **movie, TV-series and anime tracking + entertainment-intelligence platform**.

> **Everything you watch. One intelligent place.**

Scenic is not a streaming service. It remembers what a user watches, learns what they enjoy, and helps them decide what to watch next.

## Product model

Scenic is designed around three layers:

**Memory → Taste → Decision**

- **Memory** — watch history, progress, ratings, favorites, watchlist, lists, rewatches and viewing context.
- **Taste** — Entertainment DNA, genre/person/studio patterns, taste evolution and preference signals.
- **Decision** — explainable recommendations, Smart Queue, Watch Next, Ask Scenic and context-aware planning.

The academic MVP deliberately implements a smaller, testable subset first. The broader product vision is preserved in the documentation so later group work does not lose agreed features.

## Planned architecture

React + TypeScript frontend → Express + TypeScript API → PostgreSQL via Prisma.

The API communicates with a separate Python/FastAPI decision service. External metadata providers are accessed through provider adapters. The browser never connects directly to PostgreSQL or private internal services.

## Repository workflow

- 'main' — stable, demonstrable release branch.
- 'develop' — integration branch for reviewed team work.
- Short-lived branches are created from 'develop', for example:
  - 'feature/frontend-foundation'
  - 'feature/backend-foundation'
  - 'feature/ai-service-foundation'
  - 'feature/library-tracking'
  - 'fix/progress-calculation'
  - 'docs/project-presentation'
  - 'test/qa-foundation'

See [Git workflow](docs/GIT_WORKFLOW.md).

## Start here

1. Read [Project charter](PROJECT.md).
2. Read [Product vision](docs/PRODUCT_VISION.md) so the team understands Scenic beyond the MVP.
3. Review the complete [Feature matrix](docs/FEATURE_MATRIX.md).
4. Review [UI pages and routes](docs/UI_ROUTES.md).
5. Agree on team ownership in [Team workflow](docs/TEAM.md).
6. Follow [Delivery plan](PLAN.md) and [Backlog](docs/BACKLOG.md).
7. Confirm [Architecture](docs/ARCHITECTURE.md), [Data model](docs/DATA_MODEL.md) and [API design](docs/API.md).
8. Scaffold using [Project structure](docs/PROJECT_STRUCTURE.md) and [Setup](docs/SETUP.md).
9. Follow [Contributing](CONTRIBUTING.md) and [Git workflow](docs/GIT_WORKFLOW.md) for every change.
10. Use the [Presentation deck source](presentations/SCENIC_2_PROJECT_DECK.md) for proposal/final presentation work.

## Documentation map

| Document | Purpose |
|---|---|
| [PROJECT.md](PROJECT.md) | Project charter, scope, objectives and success criteria |
| [PLAN.md](PLAN.md) | Eight-week proposed implementation sequence |
| [Product vision](docs/PRODUCT_VISION.md) | Full Scenic product direction and guiding principles |
| [Feature matrix](docs/FEATURE_MATRIX.md) | Full feature catalogue with delivery phases |
| [UI routes](docs/UI_ROUTES.md) | Pages, routes, states and ownership boundaries |
| [Requirements](docs/REQUIREMENTS.md) | Testable MVP requirements and acceptance criteria |
| [Architecture](docs/ARCHITECTURE.md) | Services and system boundaries |
| [Project structure](docs/PROJECT_STRUCTURE.md) | Planned monorepo folders and ownership |
| [Data model](docs/DATA_MODEL.md) | Entities, constraints and statistics rules |
| [API design](docs/API.md) | Proposed contracts and error behavior |
| [Decision engine](docs/DECISION_ENGINE.md) | Academic deterministic recommendation baseline |
| [AI system handoff](docs/AI_SYSTEM_HANDOFF.md) | Full Scenic intelligence/AI roadmap |
| [Git workflow](docs/GIT_WORKFLOW.md) | Branching, PRs, reviews and releases |
| [Team workflow](docs/TEAM.md) | Roles, reviews and contribution evidence |
| [Backlog](docs/BACKLOG.md) | Work items and dependencies |
| [Testing](docs/TESTING.md) | Test matrix and release gates |
| [Delivery](docs/DELIVERY.md) | Deployment, rollback and demo expectations |
| [Decisions](docs/DECISIONS.md) | Architecture and scope decision log |
| [Presentation outline](docs/PRESENTATION.md) | Short speaking outline |
| [Project deck](presentations/SCENIC_2_PROJECT_DECK.md) | Detailed slide-by-slide presentation source |
| [Security](SECURITY.md) | Credentials and vulnerability handling |

## Status

**Planning and repository foundation.** Application scaffolding, database migrations, CI, production deployment and measured test evidence are not yet implemented.

## Team

Member names, group size, course constraints, submission date and hosting budget still need to be entered. Do not invent contribution evidence; link actual issues, commits, PRs, reviews and test results.

## License

No software license has been selected yet. Agree on licensing before redistributing third-party assets or code.
