# Decisions, assumptions and risks

## Decision log
| ID | Status | Decision | Rationale / next action |
|---|---|---|---|
| D01 | Initial direction | React/TypeScript web; Express/Prisma API; Python decision service | Confirm with group and lecturer |
| D02 | Proposed | PostgreSQL is authoritative application storage | Relational viewing records and aggregate queries |
| D03 | Proposed | Begin with deterministic recommendation rules | Works without an existing training dataset |
| D04 | Proposed | One repository with separate service directories | Shared contracts and simpler group integration |
| D05 | Open | Metadata provider and permitted caching | Validate coverage, quota, attribution and terms |
| D06 | Open | Authentication/session design | Decide before implementing R01 |
| D07 | Open | Runtime versions, hosting and budget | Verify compatibility during scaffolding |
| D08 | Open | Team roster, dates, marking rubric and license | Resolve at kickoff |

## Risks
| Risk | Effect | Mitigation / trigger |
|---|---|---|
| Excess scope | Incomplete core flow | Freeze P1 until R01–R10 accepted |
| Provider limits | Search unavailable | Cache where permitted; bound requests; preserve local history |
| Inconsistent contracts | Parallel work fails integration | Review schemas first; add contract tests |
| Missing episode metadata | Misleading completion | Define eligibility and display metadata limitations |
| Little recommendation data | Poor personalization | Cold-start baseline and honest explanations |
| Team availability | Missed dependencies | Shared reviewers, small tasks, weekly integration |
| Secrets in commits | Account/data exposure | Ignore local secrets; review diffs; rotate if exposed |
| Hosting restrictions | Failed final demo | Reproducible local demonstration and backup recording |

## New decision template
ID and date; status; context; options; decision; consequences; participants; affected documents; follow-up owner.

## Kickoff questions
What is the submission date? How many members? What does the rubric require? Is deployment mandatory? What budget is available? Are external metadata APIs and AI assistance allowed?
