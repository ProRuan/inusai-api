# Inusai API 2.0 --- Decision Register 03

**Date:** 2026-11-26

**Status:** Accepted foundation design (38 decisions; 117 cumulative).

Companion to Decision Registers 01--02. All IDs below have prefix F0.1-.

| ID | Choice | Accepted decision |
| --- | --- | --- |
| F0.1-D1 | B | Compatibility-oriented modern stack; candidate versions subject to verification. |
| F0.1-D2 | C | Package-specific bounded dependency ranges; exact uv.lock resolutions. |
| F0.1-D3 | B | Explicit patch-level Docker tags with distribution variant; no latest tags. |
| F0.1-D4 | B | Redis AOF every second, named volume, noeviction, private development network, health check; production security deferred. |
| F0.1-D5 | B | Custom AbstractUser, UUIDv4, unique email identity, no username, custom manager; AUTH_USER_MODEL=users.User before migrations. |
| F0.1-D6.1 | B | Count substantive function body lines (including multiline expressions and nested blocks); exclude signatures, decorators, blank lines, standalone comments and docstrings. Count all physical file lines. |
| F0.1-D6.2 | B | Ruff for applicable automated checks; review function and file limits. |
| F0.1-D6.3 | B | Explicit justified exceptions; no artificial splitting. |
| F0.1-D7.1 | B | Enable branch measurement and enforce combined coverage \>=95%. |
| F0.1-D7.2 | B | Measure application and relevant configuration code, including unexecuted modules; exclude tests, generated migrations, third-party and justified generated entry points. |
| F0.1-D7.3 | A | Global threshold; review individual modules and critical behavior. |
| F0.1-D8.1 | A | Minimal environment inventory; DEBUG determined by settings module. |
| F0.1-D8.2 | B | Fail fast for missing or malformed critical configuration. |
| F0.1-D8.3 | B | Secure production settings baseline; deployment infrastructure deferred. |
| F0.1-D8.4 | B | Standard-library logging to container streams; no sensitive data. |
| F0.1-D8.5 | B | Isolated PostgreSQL test database and Redis state; disposable CI infrastructure. |
| F0.1-D9.1 | B | Focused common/ Python package, not a Django app; extract only justified shared functionality. |
| F0.1-D9.2 | B | Normalize DRF errors and establish a small stable error vocabulary. |
| F0.1-D9.3 | C | JSON Pointer field paths, including /email; null for non-field errors. |
| F0.1-D9.4 | B | Shared cursor pagination with stable indexed endpoint-specific ordering. |
| F0.1-D9.5 | B | Focused reusable strict request validation, preserving DRF lifecycle. |
| F0.1-D9.6 | B | Local OpenAPI documentation in development/testing; disabled in production by default. |
| F0.1-D10.1 | B | Separate liveness and readiness endpoints. |
| F0.1-D10.2 | B | Separate quality, testing and schema CI jobs. |
| F0.1-D10.3 | B | Explicit technical and engineering acceptance criteria. |
| F0.1-D11.1 | B | Trim surrounding whitespace and lowercase entire email; no provider-specific transformations. |
| F0.1-D11.2 | C | Normalized storage and database-enforced case-insensitive uniqueness; field uniqueness plus Lower(email) unique constraint proposed. |
| F0.1-D11.3 | B | Inactive normal accounts by default; explicitly active superusers. |
| F0.1-D11.4 | A | Minimal identity model retaining inherited optional names and Django permissions. |
| F0.1-D11.5 | B | Select django-rest-knox now; verify, install and implement during Users; only Django identity/auth foundation in F0. |
| F0.1-D12.1 | B | Image-managed virtual environment at /opt/venv inside Docker, outside /app bind mount. |
| F0.1-D12.2 | B | Non-root app user; configurable build-time UID/GID default 1000. |
| F0.1-D12.3 | B | Inject complete connection URLs; percent-encode reserved credential characters. |
| F0.1-D12.4 | B | Redis logical database 0 for development, 1 for tests; guard destructive cleanup. |
| F0.1-D12.5 | B | Publish API on 127.0.0.1:8000 only; listen on container interface. |
| F0.1-D13.1 | B | Candidate versions now; verify resolution and runtime compatibility incrementally during implementation. |
| F0.1-D13.2 | B | Deny unauthenticated API access by default; explicit public exceptions. |
| F0.1-D13.3 | B | Infrastructure, minimal identity and common HTTP contracts only; product domains and deployment deferred. |

---

## Verification status

Design accepted, not implemented. Exact dependency resolutions, image tags,
runtime compatibility and Knox compatibility remain unverified. No repository
or migrations have been created. Candidate versions and implementation details
are recorded in Foundation Contract 01.
