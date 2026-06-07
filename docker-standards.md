---
layout: default
title: Docker Standards
---

# Docker Standards

All Asymmetric Effort projects that use containers must follow these standards.

## Base Images

Only the following base images are permitted:

| Image | Purpose |
|---|---|
| `ubuntu:24.04` | Builder stage and runtime (only when `/bin/bash` is required) |
| `gcr.io/distroless/base` (or appropriate distroless variant) | Runtime stage (default) |

No other images may be pulled from the internet. All container images must be built from these approved base images.

## Multi-Stage Build Pattern

All Dockerfiles must use a multi-stage build pattern:

1. **Builder stage**: Uses `ubuntu:24.04` to compile, install dependencies, and prepare artifacts.
2. **Runtime stage**: Uses Google Distroless as the final image. Only the minimal artifacts needed at runtime are copied from the builder stage.

```dockerfile
# Builder stage
FROM ubuntu:24.04 AS builder
# Install build dependencies, compile, etc.

# Runtime stage
FROM gcr.io/distroless/base AS runtime
COPY --from=builder /app /app
ENTRYPOINT ["/app/binary"]
```

## Runtime Shell Exception

`ubuntu:24.04` may be used as the runtime image **only** when the application absolutely requires a shell (`/bin/bash`) at runtime. This exception must be:

- Documented in the Dockerfile with a comment explaining why a shell is required.
- Approved during code review.

When `ubuntu:24.04` is used as a runtime, it must still follow a multi-stage pattern — build dependencies must not be present in the final image.

## Prohibited Practices

- Pulling third-party runtime images from Docker Hub, GitHub Container Registry, or any other registry (e.g. `node:`, `python:`, `golang:`, `nginx:`, `alpine:`).
- Using `latest` tags. All base image references must use explicit version tags or SHA digests.
- Installing unnecessary packages in the runtime stage.
- Running containers as root. A non-root `USER` must be specified in the runtime stage.
- Storing secrets, credentials, or API keys in image layers.

## Image Hardening

- Runtime images must contain only the application binary and its runtime dependencies.
- No build tools, compilers, package managers, or development libraries in the final image.
- Container health checks should be defined where applicable.
- Images must be scanned for vulnerabilities before deployment. See [Vulnerability Management](security-standards#vulnerability-management) for SLAs.
