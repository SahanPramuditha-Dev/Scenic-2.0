# Decision engine plan

> **Scope:** This file defines the deterministic recommendation baseline for the academic MVP. For the **full product AI vision**—Ask Scenic, Entertainment DNA/Memory, Scenic Match, Smart Queue, Taste Evolution, planning, semantic discovery, spoiler intelligence, availability intelligence, group recommendation and future ML—see [`AI_SYSTEM_HANDOFF.md`](AI_SYSTEM_HANDOFF.md).

## MVP approach
Start with a deterministic content-based ranking baseline. A trained ML system requires data and evaluation that the initial project may not have.

## Inputs
A bounded pool of candidate metadata; aggregate genre preferences from completed titles; already-completed IDs; optional explicit genres/runtime filters. Candidate retrieval belongs to the API/provider adapter.

## Baseline pipeline
1. Validate request schema and cap candidate count.
2. Remove duplicate IDs, excluded IDs and candidates violating explicit filters.
3. Normalize available signals to 0–1.
4. Proposed score: 0.60 genre affinity + 0.25 provider popularity + 0.15 provider rating.
5. For missing signals, renormalize available weights; never treat missing data as a perfect score.
6. Sort deterministically with title ID as the final tie-breaker.
7. Return up to the requested count and reason codes derived from actual contributing signals.

Weights are initial hypotheses to evaluate, not measured optimal values.
A watchlisted but unwatched title remains eligible.

## Cold start and fallback
Without history, use explicitly selected genres if available; otherwise use available popularity/rating signals with a “popular starting point” explanation.
If all signals are missing, use deterministic catalog order with a generic explanation.
If no candidates meet filters, return an empty result with guidance to broaden filters.
When the Python service fails, the API applies a simpler eligible-popularity ranking and identifies source=fallback.

## Evaluation
Build synthetic profiles: action fan, mixed genres, new user, all candidates watched, missing metadata and empty candidate set.
Check exclusion correctness, deterministic order, reason accuracy and latency.
Record qualitative reviewer feedback; do not claim accuracy improvements without a defined dataset and comparison.
Future experiments may add diversity reranking or feedback-based models after the baseline is accepted.
