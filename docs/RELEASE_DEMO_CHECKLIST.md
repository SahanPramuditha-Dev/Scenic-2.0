# Release and demo checklist

Use this before merging a milestone from `develop` to `main` and before the final presentation.

## Repository state

- [ ] All release work is merged into `develop`.
- [ ] No known critical defect is open.
- [ ] No secrets, real passwords or private data are committed.
- [ ] Documentation matches the implemented behavior.
- [ ] Database migrations are committed and ordered correctly.
- [ ] Lockfiles are committed.
- [ ] Known limitations are written down.

## Automated quality gates

- [ ] Frontend lint/typecheck passes.
- [ ] Backend lint/typecheck passes.
- [ ] Python formatting/lint/test checks pass.
- [ ] Unit tests pass.
- [ ] Integration tests pass.
- [ ] Cross-user authorization tests pass.
- [ ] Statistics fixture tests pass.
- [ ] Recommendation deterministic tests pass.
- [ ] Build succeeds from a clean checkout.

## Manual checks

- [ ] Register/sign in/sign out.
- [ ] Search provider catalogue.
- [ ] Open a media detail page.
- [ ] Add/remove watchlist.
- [ ] Mark movie watched idempotently.
- [ ] Track episode progress.
- [ ] Continue Watching/Up Next is correct after refresh.
- [ ] Dashboard counts match known records.
- [ ] Loading, empty and error states are visible and understandable.
- [ ] Decision-service failure does not break tracking.
- [ ] Narrow/mobile layout is usable.
- [ ] Keyboard focus and key interactions work.

## Optional P1 checks

Only tick if implemented:
- [ ] ratings/favorites;
- [ ] Entertainment DNA;
- [ ] franchise/universe released-progress rules;
- [ ] release/chronological watch-order switch;
- [ ] richer statistics;
- [ ] Smart Queue.

## Demo rehearsal

Use a synthetic demo account and rehearse:

1. Sign in.
2. Search a title.
3. Add it to the watchlist.
4. Mark a movie watched.
5. Track a series episode.
6. Show Continue Watching.
7. Show the updated dashboard/statistics.
8. Request recommendations.
9. Explain recommendation reason codes.
10. If implemented, show one franchise/universe progress example.

## Failure backup

Prepare:
- deterministic seed data;
- screenshots for critical flows;
- a provider-failure fixture or cached demo path where allowed;
- clear explanation of what is live vs mocked;
- local demo instructions if hosting fails.

## Release PR

Open `develop → main` with:
- milestone summary;
- included issues;
- verification evidence;
- known limitations;
- migration/deployment notes;
- rollback instructions when deployment exists.
