# Inusai API 2.0 — Decision Register 02

**Date:** 2026-11-25

**Status:** Accepted design baseline (D6–D10; 49 decisions)

| ID     | Accepted decision                                                                                                                                   |
| ------ | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| D6.1   | B — Latest mutually compatible stable technology versions.                                                                                          |
| D6.2   | B — Bounded dependency ranges in pyproject.toml; exact resolved versions in uv.lock.                                                                |
| D6.3   | B — Support one Python minor series; use a tested patch version in Docker.                                                                          |
| D6.4   | B — Runtime dependencies and one development dependency group.                                                                                      |
| D6.5   | B — Commit one shared uv.lock; enforce locked installations in development, CI and production.                                                      |
| D6.6   | B — Dedicated, reviewed dependency updates; prioritize security updates.                                                                            |
| D6.7   | B — Introduce dependencies for justified requirements; evaluate anticipatory additions individually.                                                |
| D7.1   | A — Four independent Compose services: api, worker, db and redis; API and worker share an application image.                                        |
| D7.2   | B — Slim Debian-based Python image and official PostgreSQL and Redis images.                                                                        |
| D7.3   | A — One simple Django Dockerfile initially; evolve when justified.                                                                                  |
| D7.4   | B — Explicit environment-specific Compose files; compose.dev.yml initially.                                                                         |
| D7.5   | B — Source bind mounts, container-managed Python environment outside the source mount, and named data volumes.                                      |
| D7.6   | B — Default Compose network; publish only the API port by default.                                                                                  |
| D7.7   | B — PostgreSQL and Redis health checks and health-based startup dependencies.                                                                       |
| D7.8   | B — Explicit database migrations; no automatic migrations or other unintended state changes at startup.                                             |
| D7.9   | B — Dedicated non-root application user.                                                                                                            |
| D8.1   | A — Development, testing and production settings inherit directly from base.py.                                                                     |
| D8.2   | B — django-environ for configuration parsing.                                                                                                       |
| D8.3   | A — One untracked local .env and committed .env.example initially; environment-specific files may be introduced later.                              |
| D8.4   | B — Infrastructure injects configuration; Django reads process environment variables only.                                                          |
| D8.5   | B — Fail fast for missing or invalid critical configuration; safe defaults for noncritical values.                                                  |
| D8.6   | C — Infrastructure initialization variables (POSTGRES\_\*) and application connection URLs (DATABASE_URL, REDIS_URL).                               |
| D8.7   | B — Environment-appropriate secrets management; no dedicated secrets manager required initially.                                                    |
| D8.8   | B — Technology-specific prefixes and established standard variable names; INUSAI\_\* for application-specific configuration.                        |
| D8.9   | B — Explicit standard-library logging with configurable verbosity and no sensitive information.                                                     |
| D9.1   | A — Resource-oriented REST; explicit domain actions where CRUD is unsuitable.                                                                       |
| D9.2   | A — URL path versioning, initially /api/v1/.                                                                                                        |
| D9.3   | A — Lowercase plural resource collections, kebab-case and trailing slashes; justified singleton and action exceptions.                              |
| D9.4   | B — UUIDv4 for independently identifiable domain resources; authorization remains mandatory.                                                        |
| D9.5   | A — snake_case JSON properties; documented representations, UTC timestamps and explicit duration units.                                             |
| D9.6   | A — Direct successful resource representations; dedicated pagination envelope.                                                                      |
| D9.7   | B — Unified error envelope: errors containing code, field (nullable) and detail; HTTP status remains authoritative.                                 |
| D9.8   | A — Standard HTTP semantics; PATCH by default, PUT where complete replacement is meaningful.                                                        |
| D9.9   | C — Cursor pagination by default, with justified and documented endpoint-specific exceptions; implement cursor pagination initially.                |
| D9.10  | B — Default page size 20, maximum 100; smaller endpoint limits where justified.                                                                     |
| D9.11  | A — Standardized search, ordering and filter parameters with explicit allowlists; ordering compatible with pagination.                              |
| D9.12  | B — Strict request validation; reject unknown and read-only fields and empty PATCH; accept valid unchanged PATCH without unnecessary state changes. |
| D9.13  | B — Generated OpenAPI with targeted explicit annotations and schema validation.                                                                     |
| D10.1  | A — Create an empty GitHub repository and initialize the project locally.                                                                           |
| D10.2  | A — Public repository without an explicit license initially.                                                                                        |
| D10.3  | B — Lightweight feature branching with main as the permanent integration branch.                                                                    |
| D10.4  | B — Purpose-based branch names, e.g. feature/users and chore/project-foundation.                                                                    |
| D10.5  | B — Conventional Commits.                                                                                                                           |
| D10.6  | A — Fast-forward-only merges; resolve divergence deliberately.                                                                                      |
| D10.7  | C — Progressive branch protection; local and remote verification before integration once CI is operational; mandatory pull requests deferred.       |
| D10.8  | B — Structured, evolutionary documentation; create files and directories when justified.                                                            |
| D10.9  | B — Small, explicitly scoped implementation milestones with human-led AI collaboration.                                                             |
| D10.10 | B — Relevant checks during milestones and full applicable verification before merging.                                                              |
| D10.11 | B — Git tags for meaningful software releases, independent of milestone identifiers.                                                                |

## Open implementation details

Exact technology versions and compatibility, Docker image tags, container
permissions, Redis persistence and authentication, environment variable
inventory, connection URL encoding, production security and logging details,
line-counting rules, line versus branch coverage, CI configuration and GitHub
protection rules remain unresolved.

Authentication and the custom user model require a decision before initial
database migrations. Authorization, CORS, throttling, error code vocabulary,
nested error paths, pagination ordering and consistency, idempotency,
concurrency, API compatibility policies and production documentation exposure
require further contracts where applicable.

No repository has been created or modified, and no implementation or dependency
compatibility has been verified as part of this design register.

## Proposed next block

- F0.1 — Foundation contract and technology compatibility.
- F0.2 — Repository initialization and engineering documentation.
- F0.3 — Python project and dependency management.
- F0.4 — Docker development infrastructure.
- F0.5 — Django project and environment configuration.
- F0.6 — Formatting, linting, testing and coverage.
- F0.7 — Common HTTP API infrastructure.
- F0.8 — GitHub Actions and continuous integration.
- F0.9 — Foundation acceptance and integration.

These milestone identifiers and their ordering are proposals, not accepted
implementation contracts. Resolve the custom user model before initial database
migrations.
