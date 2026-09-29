# Git and GitHub workflow

## Goals

Keep the group productive without breaking the demo branch, make contributions reviewable, and preserve clear evidence for assessment.

## Branches

### main
Stable milestone/release branch. It should represent the best demonstrable version of Scenic.

Do not push unfinished work directly to main.

### develop
Shared integration branch. Reviewed feature work is merged here first.

At a milestone, open a release pull request from develop to main.

### Short-lived work branches
Create from the latest develop:

- 'feature/<topic>' — user-facing or technical feature
- 'fix/<topic>' — defect correction
- 'docs/<topic>' — documentation
- 'test/<topic>' — test/QA work
- 'refactor/<topic>' — behavior-preserving cleanup

Examples:
- 'feature/episode-progress'
- 'feature/frontend-foundation'
- 'feature/backend-foundation'
- 'feature/ai-service-foundation'
- 'fix/watchlist-duplicate'
- 'docs/project-presentation'

Avoid branches named only after a person's name.

## Typical commands

    git checkout develop
    git pull origin develop
    git checkout -b feature/episode-progress

After changes:

    git add .
    git commit -m "feat: add episode progress tracking"
    git push -u origin feature/episode-progress

Then open a pull request into develop.

## Pull request rules

A PR should:
- link a GitHub issue;
- explain the user/system outcome;
- include verification steps;
- include screenshots for UI changes;
- identify API/schema/migration changes;
- stay focused enough to review;
- receive at least one peer review when team size allows.

Do not combine unrelated features into one PR.

## Integration rules

Before merging:
- update the branch with current develop if conflicts/integration changes exist;
- run relevant tests/lint/build checks;
- verify database migrations on a clean environment when applicable;
- test cross-user authorization for private data;
- confirm UI failure states for provider/AI requests.

## Release flow

1. Complete milestone scope in develop.
2. Freeze new features temporarily.
3. Run full test/demo checklist.
4. Create PR: develop → main.
5. Record known limitations.
6. Merge after team sign-off.
7. Tag releases later when versioning is introduced.

## Emergency fixes

For a release-blocking main defect:
1. branch 'fix/<topic>' from main;
2. fix and review;
3. merge to main;
4. merge/cherry-pick the same correction back to develop.

## Conflict prevention

Agree ownership before large parallel work. Changes to Prisma schema, shared types, auth middleware, global CSS/design tokens and API contracts should be communicated before multiple members edit them simultaneously.

## Branch protection

Recommended when GitHub settings permit:
- require PR before merging to main;
- require one approval;
- require passing CI checks once CI exists;
- block force-push/deletion on main.

The repository connector may not be able to configure administrative protection rules; the team can enable them in GitHub settings.
