# Scenic 2.0 presentation outline

This is the compact speaking outline. The detailed slide source is in ../presentations/SCENIC_2_PROJECT_DECK.md.

## 1. Problem — 45 seconds

People use fragmented watchlists, forget episode progress and still struggle to decide what to watch.

## 2. Scenic — 45 seconds

Scenic is a movie, TV and anime tracking + entertainment-intelligence platform.

Core idea:

**Memory → Taste → Decision**

It does not stream video.

## 3. Core user journey — 60 seconds

Discover → Save → Watch → Track → Understand taste → Decide what is next.

## 4. Experience — 90 seconds

Show Home, Discover/Search, Details, Library/Continue Watching, Statistics and Watch Next.

For a proposal, use clearly labeled mockups.
For the final presentation, replace mockups with real application screenshots/demo.

## 5. Architecture — 60 seconds

React/TypeScript → Express/TypeScript → PostgreSQL/Prisma.

Express calls a separate Python/FastAPI decision service. Explain why the API owns authentication/data and Python owns ranking/intelligence.

## 6. Intelligence — 60 seconds

MVP: deterministic recommendation ranking with explanations.

Product roadmap: Entertainment DNA, Smart Queue, Scenic Match, contextual Watch Next, Ask Scenic, spoiler intelligence and availability intelligence.

Do not present future features as already implemented.

## 7. Group workflow — 45 seconds

main = stable release.
develop = integration.
Short-lived feature branches + PR reviews + issue-linked evidence.

Show actual member responsibilities and contribution links.

## 8. Quality — 60 seconds

Authorization, idempotent tracking, statistics correctness, responsive states, tests, provider failure handling and decision-service fallback.

## 9. Roadmap/result — 45 seconds

Proposal: show milestones and the first vertical slice.
Final: show requirements delivered, test evidence, limitations and realistic next steps.

## Preparation checklist

- Confirm time/slide limit and assessment rubric.
- Replace TBD team information.
- Use actual screenshots only when implemented.
- Rehearse a fresh-machine demo.
- Prepare synthetic demo data.
- Never claim measured recommendation accuracy without evidence.
