# Skill: containerization

**Type:** atomic

## Purpose

Containerise an application or review an existing container definition such that the resulting image is minimal, secure, reproducible, and production-ready. A container that works locally but fails in production is not done.

## When to Invoke

- An application needs to be containerised for the first time.
- An existing Dockerfile or container setup needs to be reviewed for correctness or security.
- A container image is failing in production and the definition needs to be diagnosed.

## Workflow

1. **Understand the application's runtime requirements.** Before writing a Dockerfile:
   - What process does the container run?
   - What environment variables does it need?
   - What ports does it expose?
   - What volumes or file paths does it need access to?
   - What are the startup and shutdown signals it responds to?

2. **Choose the base image.** Prefer:
   - Official images from Docker Hub or the language's official registry
   - The smallest variant that meets requirements (`alpine` or `distroless` over `ubuntu`)
   - A specific digest-pinned tag — never `latest`
   Verify that the base image has no known Critical or High CVEs before using it.

3. **Minimise the image.** Every layer adds to the image size and attack surface:
   - Use multi-stage builds: build in one stage, copy only the artifact to the final stage
   - Install only what the runtime needs — not build tools
   - Remove package caches and temporary files in the same `RUN` layer that creates them
   - Do not copy unnecessary files from the build context (use `.dockerignore`)

4. **Run as a non-root user.** The container process must not run as root:
   ```dockerfile
   RUN addgroup -S appgroup && adduser -S appuser -G appgroup
   USER appuser
   ```
   Verify the application starts and operates correctly as a non-root user.

5. **Make the image reproducible.** Pin all dependency versions. Two builds from the same Dockerfile must produce the same image. Non-reproducible images make debugging and rollback unreliable.

6. **Define health checks.** The Dockerfile or orchestration config must include a health check:
   ```dockerfile
   HEALTHCHECK --interval=30s --timeout=3s CMD curl -f http://localhost:8080/health || exit 1
   ```

7. **Verify the image.** Before declaring the image done:
   - Scan the image for vulnerabilities with `trivy` or equivalent
   - Verify the process starts and responds to health checks
   - Verify the container shuts down cleanly on SIGTERM
   - Confirm no secrets are embedded in the image layers (`docker history` check)

## Output

- **Dockerfile** — minimal, reproducible, non-root, with health check
- **`.dockerignore`** — ensuring only necessary files are included in the build context
- **Scan results** — vulnerability scan output confirming no Critical or High CVEs
- **Verification record** — confirmation that the container starts, serves health checks, and shuts down cleanly
