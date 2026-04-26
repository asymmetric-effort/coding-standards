---
layout: default
title: Definition of Done
---

# Definition of Done

A task, feature, or bug fix is considered **done** when all of the following criteria are met.

## Code Quality

- Code compiles and builds without errors or warnings.
- Code follows the project's established style guidelines and linting rules.
- A strict linter standard must be enforced by git hooks locally (pre-commit) and as the first stage of remote CI/CD pipelines.
- No TODO or FIXME comments left unresolved for the current task.
- Dead code, unused imports, and unused variables have been removed.
- Strongly typed languages are preferred for all projects.
- Recursion is not allowed except where tail-call optimization is guaranteed by the language runtime.
- All queues and buffers must be bounded.

## Security

- No critical, high, or medium vulnerabilities as determined by a SAST tool appropriate to the language.
- CodeQL must be enabled on all projects.
- Dependabot must be enabled on all projects.
- OWASP and CIS standards must be met.
- All network traffic must be encrypted in flight.
- All encryption must support Post-Quantum Cryptography (PQC) (e.g. TLS 1.3+) and no less than TLS 1.2.
- For non-PQC cryptography, all solutions must use ECC.

## Testing

- At least 98% unit/integration/e2e test coverage covering both happy path and sad path.
- All existing tests pass.
- Edge cases and error paths are covered.

## Code Review

- A pull request has been opened and reviewed by at least one other team member.
- All review comments have been addressed or resolved.
- The PR description clearly explains what changed and why.

## Documentation

- Public APIs, functions, and types have clear documentation.
- All documentation must be maintained in a `docs/` directory tree and linked to be easy to find.
- Breaking changes are documented in the changelog.

## Versioning

- Projects must use tag-based semantic versioning.

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
