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
- Code formatting must be enforced by an automated formatter (e.g. Prettier) and checked in CI.
- TypeScript strict mode (or equivalent strictness for the project language) must be enabled with no suppressions.
- `const` over `let`; `var` is never permitted.
- Named exports only; default exports are not permitted.
- No `any` types unless explicitly documented and justified.
- No TODO or FIXME comments left unresolved for the current task.
- Dead code, unused imports, and unused variables have been removed.
- Strongly typed languages are preferred for all projects.
- Recursion is not allowed except where tail-call optimization is guaranteed by the language runtime. Use iterative approaches with explicit stacks.
- All queues and buffers must be bounded.
- Pure functions are preferred where possible.

## Security

- No critical, high, or medium vulnerabilities as determined by a SAST tool appropriate to the language.
- CodeQL must be enabled on all projects.
- Dependabot must be enabled on all projects for source code dependencies, and GitHub Actions dependencies.
- All GitHub Actions must be pinned to specific commit SHAs, not tags.
- OWASP and CIS standards must be met.
- All network traffic must be encrypted in flight.
- All encryption must support Post-Quantum Cryptography (PQC) (e.g. TLS 1.3+) and no less than TLS 1.2.
- For non-PQC cryptography, all solutions must use ECC.
- HTML output must be automatically escaped to prevent XSS.
- No hardcoded secrets, credentials, or API keys in source code.
- Projects should minimize runtime dependencies to reduce supply chain attack surface. Zero runtime dependencies is the ideal.
- A `SECURITY.md` policy must be present with reporting instructions and response timelines.

## Testing

- At least 98% unit/integration/e2e test coverage covering both happy path and sad path.
- All existing tests pass with zero failures.
- Edge cases and error paths are explicitly covered.
- Tests are organized into `unit/`, `integration/`, and `e2e/` directories.
- E2E tests must cover all supported browsers where applicable.
- Test-driven development is preferred: tests written before or alongside implementation.
- Coverage thresholds must be enforced in CI and must not regress.

## CI/CD Pipeline

- CI must run as a multi-stage pipeline: lint/typecheck, test, build, e2e, deploy.
- Lint and type checking must be the first stage and must block all subsequent stages.
- Build artifacts must be verified (correct outputs exist, bundle size within limits).
- All CI checks must pass before a PR can be merged.
- Post-deployment verification (smoke tests or E2E against the deployed environment) should be performed where applicable.
- Local CI execution must be supported (e.g. via `act` or equivalent) so developers can validate before pushing.

## Git Hooks

- Pre-commit hooks must enforce type checking and code formatting.
- Pre-push hooks must enforce tests and coverage thresholds.
- Hook setup must be documented and simple (e.g. symlink from `git-hooks/` to `.git/hooks/`).

## Code Review

- A pull request has been opened and reviewed by at least one other team member.
- All review comments have been addressed or resolved.
- The PR description clearly explains what changed and why.

## Documentation

- Public APIs, functions, and types have clear documentation (e.g. JSDoc, GoDoc, or equivalent).
- All documentation must be maintained in a `docs/` directory tree, organized by topic, and linked from an index page.
- Documentation must use GitHub-flavored Markdown with language-tagged code blocks.
- One concept per page; use relative internal links.
- Breaking changes are documented in a `CHANGELOG.md`.
- A `CONTRIBUTING.md` must be present with setup instructions, development workflow, and coding conventions.
- A `CODE_OF_CONDUCT.md` must be present in all projects.

## Versioning and Commits

- Projects must use tag-based semantic versioning.
- Commit messages must follow Conventional Commits format: `feat:`, `fix:`, `test:`, `docs:`, `refactor:`, `perf:`, `chore:`.

## Integration

- The branch is rebased on the latest target branch with no merge conflicts.
- CI pipeline passes all stages (build, lint, test, security checks).
- No regressions introduced in existing functionality.

## Licensing and Intellectual Property

- All code must be original work or covered by an MIT-compatible license.
- No code may be copied without license verification.
- Third-party assets (fonts, icons, data) must have explicit permission or compatible licensing.
- A `ThirdPartyNotices.txt` or equivalent must be maintained if any third-party components are used.

## Deployment Readiness

- Feature flags or configuration changes are documented.
- Database migrations (if any) are reversible and tested.
- Monitoring and alerting are in place for new components or endpoints.

## Acceptance

- The work satisfies the requirements defined in the issue or ticket.
- The feature has been verified in a staging or preview environment where applicable.
- Product owner or stakeholder has approved the work (when required).
