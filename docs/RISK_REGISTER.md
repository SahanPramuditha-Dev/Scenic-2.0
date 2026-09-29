# Scenic 2.0 — Risk register

Review this at least once per week and before milestone releases.

| ID | Risk | Likelihood | Impact | Early warning | Mitigation / response | Owner |
|---|---|---|---|---|---|---|
| R01 | MVP scope grows faster than team capacity | High | High | P1/P2 work starts while P0 flows are incomplete | Freeze MVP; require issue + acceptance criteria; defer optional work | TBD |
| R02 | Frontend/backend/AI are developed separately and integrate late | Medium | High | mocked contracts differ; integration postponed | Deliver vertical slices; agree contracts early; integration demo weekly | TBD |
| R03 | Prisma/schema conflicts across members | Medium | High | multiple migrations touch same entities | appoint schema reviewer; communicate shared-model changes before coding | TBD |
| R04 | Authentication/authorization is incomplete | Medium | Critical | user IDs accepted from client; cross-user tests absent | centralize auth; server derives user identity; add cross-user tests | TBD |
| R05 | Metadata provider limits or inconsistent episode data | Medium | High | quota errors; missing specials/air dates | provider adapter; cache where appropriate; defensive mapping; documented fallback fixtures | TBD |
| R06 | AI scope becomes an untestable chatbot project | High | High | LLM added before deterministic baseline | begin with filters + ranking + reason codes; add LLM only where it adds value | TBD |
| R07 | Statistics disagree with tracking state | Medium | High | dashboard counts differ after refresh | define canonical event/state rules; fixture-based aggregate tests | TBD |
| R08 | Team members work on long-lived divergent branches | Medium | Medium | large merge conflicts; branches weeks behind develop | small PRs; regularly update from develop; delete merged work branches | TBD |
| R09 | Demo depends on live external APIs/internet | Medium | High | unstable provider response during rehearsal | prepare synthetic seed/demo data and safe fallback mode | TBD |
| R10 | Secrets or personal data enter repository/history | Low | Critical | `.env` staged; real account data used in fixtures | .gitignore, secret review, synthetic data only, immediate key rotation | TBD |
| R11 | CI is added too early with fake/nonexistent commands | Medium | Medium | workflow green but does not test real code | add CI only after actual scripts exist; fail on lint/typecheck/tests | TBD |
| R12 | Presentation claims features not implemented | Medium | High | slides use future features as completed evidence | label MVP/P1/P2 clearly; use real demo evidence only | TBD |
| R13 | Franchise/universe progress becomes inconsistent | Medium | Medium | provider collection membership conflicts with Scenic logic | Scenic owns versioned membership/order rules; show denominator policy | TBD |
| R14 | Final week is consumed by new features | High | High | feature PRs continue during stabilization | feature freeze before release; defects/docs/testing only | TBD |

## Severity rule

Critical risks receive immediate team attention. High-impact risks should have a named owner before the related implementation begins.

## Update format

When a risk changes, record:
- date;
- new likelihood/impact;
- evidence;
- mitigation action;
- owner;
- next review date.
