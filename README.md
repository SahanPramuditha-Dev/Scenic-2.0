# Scenic 2.0

Scenic 2.0 is a group project for building a **movie, TV-series and anime tracking + entertainment-intelligence platform**.

> **Everything you watch. One intelligent place.**

Scenic is not a streaming service. It remembers what a user watches, learns what they enjoy, and helps them decide what to watch next.

## Product model

Scenic is designed around three layers:

**Memory → Taste → Decision**

- **Memory** — watch history, progress, ratings, favorites, watchlist, lists, rewatches, franchise/universe progress, watch orders and viewing context.
- **Taste** — Entertainment DNA, genre/person/studio patterns, taste evolution and preference signals.
- **Decision** — explainable recommendations, Smart Queue, Watch Next, Ask Scenic and context-aware planning.

The academic MVP deliberately implements a smaller, testable subset first. The broader product vision is preserved in the documentation so later group work does not lose agreed features.

## Planned architecture

React + TypeScript frontend → Express + TypeScript API → PostgreSQL via Prisma.

The API communicates with a separate Python/FastAPI decision service. External metadata providers are accessed through provider adapters. The browser never connects directly to PostgreSQL or private internal services.

## Repository workflow

- `main` — stable, demonstrable release branch.
- `develop` — integration branch for reviewed team work.
- Initial workstream branches:
  - `feature/frontend-foundation`
  - `feature/backend-foundation`
  - `feature/ai-service-foundation`
  - `feature/tracking-core`
  - `feature/franchise-universe-tracking`
  - `test/qa-foundation`
  - `chore/ci-cd-foundation`
  - `docs/project-presentation`
- Normal feature work should move to short-lived issue-specific branches from `develop`, such as `feature/episode-progress` or `fix/progress-calculation`.

See [Git workflow](docs/GIT_WORKFLOW.md) and [Group execution plan](docs/GROUP_EXECUTION_PLAN.md).

## Start here

1. Read [Project charter](PROJECT.md).
2. Read [Product vision](docs/PRODUCT_VISION.md) so the team understands Scenic beyond the MVP.
3. Review the complete [Feature matrix](docs/FEATURE_MATRIX.md).
4. Review [UI pages and routes](docs/UI_ROUTES.md).
   - For the product-level recommendation behavior behind Watch Next/Ask Scenic, read the [contextual recommendation specification](docs/CONTEXT_AWARE_RECOMMENDATIONS.md).
5. Read [Group execution plan](docs/GROUP_EXECUTION_PLAN.md).
6. Complete [Team onboarding](docs/TEAM_ONBOARDING.md) and agree ownership in [Team workflow](docs/TEAM.md).
7. Follow [Delivery plan](PLAN.md) and [Backlog](docs/BACKLOG.md).
8. Confirm [Architecture](docs/ARCHITECTURE.md), [Data model](docs/DATA_MODEL.md) and [API design](docs/API.md).
9. Complete the [Engineering foundation](docs/ENGINEERING_FOUNDATION.md) before substantial feature development.
10. Scaffold using [Project structure](docs/PROJECT_STRUCTURE.md), [Setup](docs/SETUP.md) and [Environment strategy](docs/ENVIRONMENT_STRATEGY.md).
11. Follow [Contributing](CONTRIBUTING.md) and [Git workflow](docs/GIT_WORKFLOW.md) for every change.
12. Review the [Risk register](docs/RISK_REGISTER.md) during weekly integration.
13. Use [Release/demo checklist](docs/RELEASE_DEMO_CHECKLIST.md) before milestone releases.
14. Use the [Project deck](presentations/SCENIC_2_PROJECT_DECK.md) for proposal/final work and [Group kickoff deck](presentations/SCENIC_2_GROUP_KICKOFF.md) for team alignment.

## Documentation map

| Document | Purpose |
|---|---|
| [PROJECT.md](PROJECT.md) | Project charter, scope, objectives and success criteria |
| [PLAN.md](PLAN.md) | Eight-week proposed implementation sequence |
| [Group execution plan](docs/GROUP_EXECUTION_PLAN.md) | Workstreams, vertical slices, sprint checkpoints and handoffs |
| [Team onboarding](docs/TEAM_ONBOARDING.md) | New-member setup and working checklist |
| [Product vision](docs/PRODUCT_VISION.md) | Full Scenic product direction and guiding principles |
| [Feature matrix](docs/FEATURE_MATRIX.md) | Full feature catalogue with delivery phases |
| [UI routes](docs/UI_ROUTES.md) | Pages, routes, states and ownership boundaries |
| [Requirements](docs/REQUIREMENTS.md) | Testable MVP requirements and acceptance criteria |
| [Architecture](docs/ARCHITECTURE.md) | Services and system boundaries |
| [Project structure](docs/PROJECT_STRUCTURE.md) | Planned monorepo folders and ownership |
| [Engineering foundation](docs/ENGINEERING_FOUNDATION.md) | Pre-development initialization checklist, tooling, UI system, database, testing, CI and first vertical slice |
| [Data model](docs/DATA_MODEL.md) | Entities, constraints and statistics rules |
| [API design](docs/API.md) | Proposed contracts and error behavior |
| [Decision engine](docs/DECISION_ENGINE.md) | Academic deterministic recommendation baseline |
| [Context-aware recommendations](docs/CONTEXT_AWARE_RECOMMENDATIONS.md) | Time-aware decisions, Watch Modes, Taste Profiles, Smart Queue lanes, refinement, feedback and recommendation memory |
| [AI system handoff](docs/AI_SYSTEM_HANDOFF.md) | Full Scenic intelligence/AI roadmap |
| [Franchise & universe tracking](docs/FRANCHISE_UNIVERSE_TRACKING.md) | Versioned universe hierarchy, watch orders, title relations, advanced status and progress rules |
| [Environment strategy](docs/ENVIRONMENT_STRATEGY.md) | Local/test/demo environments, data, migrations and provider behavior |
| [Risk register](docs/RISK_REGISTER.md) | Delivery, technical and integration risks with mitigations |
| [Git workflow](docs/GIT_WORKFLOW.md) | Branching, PRs, reviews and releases |
| [Team workflow](docs/TEAM.md) | Roles, reviews and contribution evidence |
| [Backlog](docs/BACKLOG.md) | Work items and dependencies |
| [Testing](docs/TESTING.md) | Test matrix and release gates |
| [Delivery](docs/DELIVERY.md) | Deployment, rollback and demo expectations |
| [Release/demo checklist](docs/RELEASE_DEMO_CHECKLIST.md) | Final release gate and rehearsal sequence |
| [Decisions](docs/DECISIONS.md) | Architecture and scope decision log |
| [Presentation outline](docs/PRESENTATION.md) | Short speaking outline |
| [Project deck](presentations/SCENIC_2_PROJECT_DECK.md) | Detailed slide-by-slide proposal/final presentation source |
| [Group kickoff deck](presentations/SCENIC_2_GROUP_KICKOFF.md) | Concise team kickoff presentation |
| [Security](SECURITY.md) | Credentials and vulnerability handling |

## Status

**Planning and repository foundation.** Application scaffolding, database migrations, CI, production deployment and measured test evidence are not yet implemented.

## Team

Member names, group size, course constraints, submission date and hosting budget still need to be entered. Do not invent contribution evidence; link actual issues, commits, PRs, reviews and test results.

## License

No software license has been selected yet. Agree on licensing before redistributing third-party assets or code.
