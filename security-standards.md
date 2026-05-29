---
layout: default
title: Security Standards
---

# Security Standards

All Asymmetric Effort projects must meet the following security standards. These requirements are aligned with **OWASP**, **CIS**, **HIPAA**, **SOC 2**, and **GDPR** frameworks. Every task must also satisfy the [Definition of Done](definition-of-done), which includes a security checklist derived from these standards.

## Authentication and Access Control

- All systems must enforce multi-factor authentication (MFA) for privileged accounts.
- Role-based access control (RBAC) must be implemented with least-privilege principles.
- Service accounts must use short-lived, automatically rotated credentials.
- Session tokens must be cryptographically random, stored securely (server-side or encrypted cookies), and invalidated on logout.
- Session idle timeout must not exceed 15 minutes for sensitive systems.
- Failed login attempts must be rate-limited and logged. Account lockout or escalating delays must be enforced after repeated failures.
- Password policies must require a minimum of 14 characters with no maximum length restrictions. Passwords must be checked against known-breached password lists (e.g. HIBP).
- Default credentials must never be used in any environment.
- Authentication tokens must never appear in URLs, logs, or error messages.

## Data Protection

### Encryption in Transit

- All network communication must use TLS 1.2 or higher. TLS 1.3 with post-quantum cryptography (PQC) support is preferred.
- Non-PQC cryptography must use ECC-based cipher suites. RSA and legacy ciphers (RC4, 3DES, MD5-based MACs) are prohibited.
- HSTS headers must be set with a minimum `max-age` of one year and `includeSubDomains`.
- Certificate pinning should be used for mobile applications and service-to-service communication where feasible.

### Encryption at Rest

- All sensitive data must be encrypted at rest using AES-256 or equivalent.
- Encryption keys must be managed through a dedicated key management service (KMS). Keys must never be stored alongside the data they protect.
- Key rotation must occur at least annually, with automated rotation preferred.
- Database backups must be encrypted with the same standards as production data.

### Data Classification and Handling

- All data must be classified as **Public**, **Internal**, **Confidential**, or **Restricted**.
- Personally identifiable information (PII) and protected health information (PHI) must be classified as Restricted.
- Restricted data must not be stored in logs, error messages, analytics, or development environments unless anonymized or pseudonymized.
- Data retention policies must be defined and enforced for each data classification level.
- Data must be deletable upon request to comply with GDPR right-to-erasure requirements. Deletion must be verifiable.

## Input Validation and Output Encoding

- All user input must be validated on the server side. Client-side validation is supplementary only.
- Input validation must use allowlists (not denylists) wherever possible.
- All HTML output must be contextually escaped to prevent XSS (HTML body, attributes, JavaScript, CSS, and URL contexts each require distinct encoding).
- SQL queries must use parameterized statements or prepared statements. String concatenation for query construction is prohibited.
- File uploads must validate file type by content inspection (not just extension), enforce size limits, and store files outside the web root.
- HTTP headers must include `Content-Security-Policy`, `X-Content-Type-Options: nosniff`, `X-Frame-Options: DENY`, and `Referrer-Policy: strict-origin-when-cross-origin`.
- API endpoints must validate and reject unexpected fields, enforce strict schema validation, and return minimal error detail to clients.

## Secrets Management

- No secrets, credentials, API keys, or tokens may be committed to source control. See [Definition of Done: Security](definition-of-done#security).
- A pre-commit hook must scan for secrets using a tool such as `gitleaks`, `trufflehog`, or equivalent. See [Git Hooks](definition-of-done#git-hooks) for hook enforcement requirements.
- Secrets must be stored in a dedicated secrets manager (e.g. HashiCorp Vault, AWS Secrets Manager, or equivalent).
- Secrets must be injected at runtime via environment variables or mounted files, never baked into container images or build artifacts.
- All secrets must be rotated on a defined schedule and immediately upon suspected compromise.

## Logging and Monitoring

- All authentication events (success, failure, logout, MFA challenges) must be logged.
- All authorization failures and privilege escalation attempts must be logged.
- All administrative actions and configuration changes must be logged.
- Logs must include timestamp (UTC), actor identity, action performed, resource affected, source IP, and outcome (success/failure).
- Logs must never contain passwords, tokens, session IDs, PII, or PHI.
- Logs must be stored in a tamper-evident, append-only system and retained for a minimum of one year.
- Real-time alerting must be configured for anomalous patterns: brute-force attempts, unusual access times, privilege escalations, and data exfiltration indicators.
- Log access must be restricted and itself audited.

## Vulnerability Management

- Static application security testing (SAST) must be integrated into CI/CD. No critical or high findings may be merged. See [CI/CD Pipeline](definition-of-done#cicd-pipeline) for pipeline stage requirements.
- CodeQL must be enabled on all repositories.
- Dependabot (or equivalent) must be enabled for source code dependencies and GitHub Actions dependencies.
- All GitHub Actions must be pinned to specific commit SHAs, not tags.
- Container images must be scanned for vulnerabilities before deployment. No critical or high CVEs may ship.
- Runtime dependencies must be minimized. Zero runtime dependencies is the ideal. See [Definition of Done: Security](definition-of-done#security) for the per-task checklist.
- A vulnerability disclosure and response process must be documented in `SECURITY.md` with defined SLAs:
  - **Critical**: patch within 24 hours.
  - **High**: patch within 72 hours.
  - **Medium**: patch within 30 days.
  - **Low**: patch within 90 days.

## Infrastructure and Network Security

- All infrastructure must be defined as code (IaC) and version-controlled.
- Network segmentation must isolate production, staging, and development environments.
- Firewalls and security groups must follow deny-by-default rules. Only explicitly required ports and protocols may be opened.
- Administrative interfaces must not be exposed to the public internet.
- All servers and containers must run with non-root users by default.
- Host-based intrusion detection (e.g. OSSEC, Falco) must be deployed on production systems.
- DNS must use DNSSEC where supported.
- All publicly facing services must be protected by a web application firewall (WAF) or equivalent.

## API Security

- All APIs must require authentication. Anonymous access must be explicitly justified and documented.
- API rate limiting must be enforced per client and per endpoint.
- API responses must not expose internal implementation details, stack traces, or verbose error messages.
- APIs must validate `Content-Type` headers and reject unexpected media types.
- CORS policies must be explicit and restrictive. Wildcards (`*`) in `Access-Control-Allow-Origin` are prohibited for authenticated endpoints.
- GraphQL endpoints must enforce query depth limits, complexity limits, and introspection must be disabled in production.

## Incident Response

- An incident response plan must be documented, reviewed annually, and tested at least once per year through tabletop exercises or simulations.
- Incident classification must follow a defined severity matrix with escalation paths.
- Affected individuals must be notified within 72 hours of a confirmed breach involving personal data (GDPR Article 33).
- HIPAA-covered incidents must be reported to HHS within 60 days.
- Post-incident reviews must be conducted within 5 business days of resolution, and findings must be tracked to closure.

## Privacy and Compliance

### GDPR

- A lawful basis for processing must be documented for all personal data.
- Consent must be freely given, specific, informed, and unambiguous. Pre-checked boxes are prohibited.
- Data subjects must be able to access, rectify, port, and erase their data through documented processes.
- Data processing agreements (DPAs) must be in place with all third-party processors.
- Privacy impact assessments (PIAs) must be conducted before launching features that process personal data in new ways.

### HIPAA

- PHI must only be accessible to authorized personnel with a documented need.
- Business associate agreements (BAAs) must be in place with all vendors handling PHI.
- PHI must never be transmitted over unencrypted channels.
- Audit trails for PHI access must be maintained and reviewed regularly.
- Workforce training on HIPAA requirements must be completed annually.

### SOC 2

- Change management procedures must be documented and followed for all production changes.
- Logical access reviews must be conducted quarterly.
- System availability must be monitored continuously with defined SLAs.
- Risk assessments must be performed annually and findings must be tracked to remediation.
- Vendor security assessments must be conducted before onboarding and reviewed annually.

## Secure Development Lifecycle

- Threat modeling must be performed for new features, services, and significant architectural changes.
- Security requirements must be defined during planning, not added retroactively.
- Code reviews must include explicit security review for authentication, authorization, input handling, and data exposure. See [Code Review](definition-of-done#code-review) for general review requirements.
- Third-party libraries must be evaluated for security posture, maintenance status, and license compatibility before adoption. See [Licensing and Intellectual Property](definition-of-done#licensing-and-intellectual-property) for license requirements.
- Production data must never be used in development or testing environments unless fully anonymized.
- All deployments must be reproducible from source control. No manual changes to production systems. See [Deployment Readiness](definition-of-done#deployment-readiness) for deployment checklist items.
