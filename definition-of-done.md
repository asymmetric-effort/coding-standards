---
layout: default
title: Definition of Done
---

# Definition of Done

A task, feature, or bug fix is considered **done** when all of the following criteria are met.

## Code Quality

- Code compiles and builds without errors or warnings.
- Code follows the project's established style guidelines and linting rules.
- No TODO or FIXME comments left unresolved for the current task.
- Dead code, unused imports, and unused variables have been removed.

## Testing

- Unit tests are written for all new or modified logic.
- All existing tests pass.
- Edge cases and error paths are covered.
- Test coverage meets or exceeds the project's minimum threshold.

## Code Review

- A pull request has been opened and reviewed by at least one other team member.
- All review comments have been addressed or resolved.
- The PR description clearly explains what changed and why.

## Documentation

- Public APIs, functions, and types have clear documentation.
- README or relevant docs are updated if behavior changes.
- Breaking changes are documented in the changelog.

## Integration

- The branch is rebased on the latest target branch with no merge conflicts.
- CI pipeline passes (build, lint, test, security checks).
- No regressions introduced in existing functionality.

## Deployment Readiness

- Feature flags or configuration changes are documented.
- Database migrations (if any) are reversible and tested.
- Monitoring and alerting are in place for new components or endpoints.

## Acceptance

- The work satisfies the requirements defined in the issue or ticket.
- The feature has been verified in a staging or preview environment where applicable.
- Product owner or stakeholder has approved the work (when required).
