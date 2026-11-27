# Inusai API 2.0 --- Foundation Contract 01

**Date:** 2026-11-26\
**Status:** Approved design; implementation and verification pending.

## 1. Purpose and authority

Think big. Start simple. Build iteratively. Build a modern, performant, secure, clean, maintainable and scalable learning platform while learning software engineering. Decision Registers 01--03 (117 decisions) are authoritative; this contract consolidates them. Product vision is not a binding feature contract. Resolve conflicts or deviations explicitly with the user.

## 2. Architecture and repository

Evolutionary modular monolith, one primary PostgreSQL database, Redis and Django RQ from the start. Flat ecosystem of independent fresh repositories; selectively reuse proven Generation 1 code. Rename/archive legacy repositories (proposed names inusai-api-legacy and inusai-web-legacy). Public GitHub repository without explicit license initially. Independent Semantic Versioning, HTTP API versions and milestone identifiers. Traditional Django layout; flat apps/ domains, file-first organization, pragmatic services, extract shared code on demand. Application-local tests and repository-level integration/acceptance tests.

Target layout (create only when needed): apps/users/, common/api/, config/settings/{base,development,testing,production}.py, docker/django/Dockerfile, docs/, tests/, .github/workflows/, manage.py, compose.dev.yml, pyproject.toml, uv.lock, .env.example, .gitignore, .dockerignore, README.md, AGENTS.md.

## 3. Technology and dependency policy

The following are previously agreed candidate versions, not independently reverified in this document generation turn.

---

Component Candidate

---

Python 3.14.10; support one minor series (3.14)

Django 6.0.10

DRF 3.18.3

PostgreSQL 18.7

Redis 8.10.3

django-environ 0.14.0

pytest-django 4.14.0

psycopg\[binary\] compatible 3.x

django-rq, drf-spectacular, sidecar latest mutually compatible stable

Ruff, pytest, pytest-cov, uv latest mutually compatible stable; exact versions pending

django-rest-knox selected; compatibility and installation deferred to Users

---

Use uv, bounded package-specific ranges (e.g. selected Django minor series), runtime dependencies and one development group, committed uv.lock and locked installations in development, CI and production. Dedicated reviewed dependency updates; prioritize security. Add packages only for justified requirements. Verify release metadata, support windows and actual resolution; report incompatibilities before changing baseline. Review Django upgrade timing before the previously identified April 2027 support deadline (recheck official lifecycle).

## 4. Docker and configuration

Four independent services api, worker, db, redis. API and worker share one simple Debian slim application image; candidate tags python:3.14.10-slim-trixie, postgres:18.7-trixie, redis:8.10.3-trixie; official Astral uv image explicitly pinned. Verify exact tags before use. Explicit patch/distribution tags, no floating latest. compose.dev.yml initially. Bind mount repository to /app; install image-managed dependencies at /opt/venv, outside mount. Non-root app user with configurable build-time UID/GID default 1000. Named PostgreSQL and Redis data volumes. Default private Compose network; publish only API on 127.0.0.1:8000, listening on container interface. Health checks and health-based startup dependencies. Migrations explicit, never automatic on startup. Redis AOF every second, noeviction, no published port; no password required in private development network. Production authentication, TLS, backup and operational policy deferred.

Four settings modules; development/testing/production inherit directly from base. Infrastructure injects process environment; Django uses django-environ and never reads .env directly. Untracked local .env and committed .env.example. Fail fast for critical missing/invalid values; safe documented defaults for noncritical settings. DEBUG determined by settings module. Secure production defaults for secrets, hosts, cookies and HTTPS; proxy trust, HSTS rollout and deployment details deferred.

---

Variable Purpose

---

DJANGO_SETTINGS_MODULE settings selection

DJANGO_SECRET_KEY cryptographic secret

DJANGO_ALLOWED_HOSTS allowed hosts

DJANGO_LOG_LEVEL verbosity

DATABASE_URL complete PostgreSQL URL

REDIS_URL complete Redis URL

POSTGRES_DB, POSTGRES_USER, POSTGRES_PASSWORD database initialization

---

Use established technology prefixes and INUSAI\_\* for application-specific settings. Percent-encode reserved credential characters in URLs. Environment-appropriate secrets management; no committed secrets. Standard-library logging to container streams with timestamp, severity, logger and message; no passwords, tokens, secrets or sensitive bodies.

## 5. Minimal user identity

Before initial migrations set AUTH_USER_MODEL=users.User. Custom AbstractUser with UUIDv4 primary key, no username, email as USERNAME_FIELD, custom email manager. Trim and lowercase entire email (deliberate product policy); no provider-specific dot or plus transformations. Database-enforced case-insensitive uniqueness; proposed unique email field plus Lower(email) functional unique constraint. Verify normalization and uniqueness across supported creation paths, including concurrent creation. Normal accounts inactive by default; superusers explicitly active. Retain password, optional first_name/last_name, is_active, is_staff, is_superuser, date_joined, last_login, groups and user_permissions. Django password hashing and permissions. No profile or lifecycle metadata yet. Knox selected, but no Knox installation, token endpoints or client authentication implementation in F0. Registration, activation, sessions and account management belong to Users.

## 6. Engineering and verification

69-character lines, single quotes, four spaces, sorted imports, formatter-managed trailing commas. Standard Python/Django naming; meaningful interface annotations; minimal intention-oriented comments. One coherent task per function, maximum 14 substantive body lines and 400 physical lines per file. Count multiline expressions and nested blocks; exclude signatures, decorators, blank lines, standalone comments and docstrings from function count. Ruff automated formatting, linting and security rules; length limits reviewed, exceptions explicitly justified (e.g. generated migrations). No artificial splitting. Specialized security scanners deferred.

pytest, pytest-django, pytest-cov; meaningful tests each milestone. PostgreSQL for database-dependent tests; Django-managed isolated test database. Redis DB 0 development, DB 1 tests; guard destructive cleanup, logical DBs are not security boundaries. Disposable CI infrastructure. Enable branch measurement and enforce global combined coverage \>=95%; include application and relevant configuration, including unexecuted modules; exclude tests, generated migrations, third-party code and justified generated entry points. Review module coverage and critical authentication, authorization, ownership, transactions and validation independently of percentage.

## 7. HTTP API foundation

Resource-oriented REST, explicit actions where CRUD unsuitable; /api/v1/, lowercase plural kebab-case collections with trailing slashes, justified singleton/action exceptions. UUIDv4 for independently identifiable domain resources, mandatory authorization. snake_case JSON, UTC timestamps, explicit duration units. Direct successful representations; standard HTTP semantics, PATCH by default, PUT for meaningful complete replacement.

Common Python package common/api/ (not an installed app); focused exceptions, pagination and validation modules when justified. Deny unauthenticated API access by default, explicitly permit public exceptions. No public domain endpoints until authentication/authorization contracts exist.

Unified error envelope: errors array of code, field (nullable), detail; HTTP status authoritative. JSON Pointer field paths (e.g. /email, /cards/0/front), null for non-field errors. Normalize DRF errors; initial vocabulary candidates: required, invalid, unknown_field, read_only, empty_patch, not_authenticated, permission_denied, not_found, throttled, server_error. Unexpected errors must not disclose internal details. Domain codes added with domain contracts.

Cursor pagination by default; documented endpoint-specific exceptions. page_size default 20, max 100 (smaller limits justified), cursor parameter, next/previous/results envelope, no total count by default. Stable indexed endpoint-specific ordering; no snapshot consistency promise. Standard search, ordering and filter parameters with explicit allowlists compatible with pagination. Reject unknown/read-only input fields and empty PATCH; accept valid unchanged PATCH without unnecessary state changes. Reusable strict validation preserving DRF lifecycle; domain-specific rules remain local.

Generated OpenAPI with targeted annotations and schema validation. /api/schema/, /api/docs/, /api/redoc/ in development/testing; disabled in production by default; local sidecar assets. Operational /health/live/ confirms HTTP responsiveness; /health/ready/ checks required PostgreSQL and Redis connections; minimal responses, no infrastructure disclosure. These are outside versioned domain resources.

## 8. Workflow and CI

Human-led design, ChatGPT architecture/review, Codex scoped implementation, automated verification. Explore → Decide → Define → Implement → Review → Verify → Learn → Commit. Empty GitHub repository, initialize locally; permanent main, lightweight purpose-based branches (e.g. chore/project-foundation), Conventional Commits, fast-forward-only integration, deliberate divergence resolution. Progressive branch protection, local and remote checks before integration once CI operational; mandatory PRs deferred. Git tags for meaningful releases. Evolutionary documentation. Separate GitHub Actions quality (Ruff), testing (pytest/coverage), schema (Django checks/OpenAPI validation) jobs, locked dependencies and compatible services. Relevant checks each milestone, full applicable checks before merge.

## 9. Acceptance and boundaries

F0 includes repository, dependency management, Docker, Django settings, minimal user model, quality engineering, common HTTP infrastructure, health, OpenAPI and CI. Acceptance requires fresh clone and locked install, four services operational, PostgreSQL/Redis connectivity, explicit migrations, worker job execution, environment validation and production settings checks, HTTP contracts and health tests, schema validation, Ruff checks, all tests passing and coverage \>=95%, successful CI, reviewed README/AGENTS.md, no committed secrets or unresolved critical defects.

Deferred: Knox implementation, registration/activation, account management, all product domains, CORS/throttling and domain-specific authorization/idempotency/concurrency policies where applicable, production deployment. Exact versions, image availability, runtime compatibility, CI implementation and deployment-specific security remain unverified. See F0 roadmap for verification gates.
