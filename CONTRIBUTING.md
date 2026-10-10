# Contributing to OutcomeHub

This repository is a four-person university team project. The workflow is intentionally simple so that work stays attributable, reviewable, and easy to explain in CSE 311.

## Workflow

1. Pick or create a GitHub issue.
2. Assign the issue to yourself.
3. Create a branch from `main`.
4. Make focused commits.
5. Push the branch.
6. Open a pull request that references the issue.
7. Ask at least one teammate to review it when practical.
8. Merge only after the change is in a usable state.

## Branch naming

Use a short prefix plus the issue number and task name.

Examples:

```text
feature/3-user-roles
feature/13-lo-calculation
fix/17-student-results
chore/1-django-setup
```

## Commit messages

Prefer short messages that explain the change.

Examples:

```text
feat: add ProgramOutcome model
fix: normalize LO weights during score calculation
test: add weighted score tests
docs: update architecture diagram
chore: configure CI
```

Avoid vague messages such as `stuff`, `changes`, or `final`.

## Pull requests

A pull request should:

- explain what changed
- link the issue, e.g. `Closes #13`
- mention how the change was tested
- stay focused on one task when possible

Suggested template:

```markdown
## What changed

- ...

## Why

- ...

## Testing

- ...

Closes #...
```

## Definition of done

An issue is done when:

- the requested behavior works
- relevant tests pass or a reason is documented
- no secrets or local-only files are committed
- documentation is updated if the architecture/behavior changed
- the change is merged through a pull request when practical

## Team evidence

Because the project is also evaluated on process, everyone should use their own GitHub account and make attributable contributions through issues, commits, reviews, and pull requests. Do not funnel the whole project through one person's account.
