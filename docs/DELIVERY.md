# Deployment and demonstration

Hosting selection and budget are TBD. This is a release procedure to implement, not a live deployment.

## Before release
1. Choose hosts supporting the web, Node API, private Python service and PostgreSQL.
2. Configure production secrets through host secret storage.
3. Set allowed origins, secure session settings, TLS and provider attribution.
4. Run CI against the exact release commit.
5. Back up the database and rehearse restoring a non-production copy.
6. Apply reviewed migrations as a controlled release step.
7. Deploy compatible API and decision versions, then web assets.
8. Verify health, authentication, save/progress actions and recommendation fallback.

## Rollback
Record previous application versions and database migration compatibility before deployment.
Prefer backward-compatible migrations. Do not automatically reverse destructive migrations.
If release fails, restore prior application versions when schema-compatible; otherwise follow a reviewed recovery plan using the backup and documented data-loss window.

## Demonstration script
1. Explain the fragmented watchlist/choice problem.
2. Sign in with a synthetic demo account.
3. Search for a movie and add it to the watchlist.
4. Mark it watched and show the dashboard change.
5. Mark an episode and show season progress.
6. Show recommendation reasons.
7. Demonstrate the controlled unavailable-service fallback.
8. Explain architecture, team contributions and known limitations.

Keep synthetic local demo data and a short recorded backup if permitted by the assessment. Never display production secrets or real users' records.
