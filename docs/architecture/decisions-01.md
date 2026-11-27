# Inusai API 2.0 — Decision Register 01

**Date:** 2026-11-24  
**Status:** Accepted design baseline (D1–D5; 30 decisions)

| ID   | Accepted decision                                                                                                                   |
| ---- | ----------------------------------------------------------------------------------------------------------------------------------- |
| D1   | B — Evolutionary modular monolith; one primary relational database; abstractions on demand.                                         |
| D2.1 | C — Fresh repositories; selectively reuse proven code.                                                                              |
| D2.2 | A — Flat ecosystem structure with independent repositories.                                                                         |
| D2.3 | B — Independent Semantic Versioning; product generation, milestones and HTTP API versions remain separate.                          |
| D2.4 | B — Rename and archive Generation 1. Proposed names: inusai-api-legacy and inusai-web-legacy.                                       |
| D3.1 | A — Python and Django.                                                                                                              |
| D3.2 | A — Django REST Framework.                                                                                                          |
| D3.3 | A — PostgreSQL.                                                                                                                     |
| D3.4 | A — Redis and Django RQ from the beginning.                                                                                         |
| D3.5 | B — uv for dependency and environment management.                                                                                   |
| D3.6 | B — Docker-first development.                                                                                                       |
| D3.7 | A — Ruff, pytest, pytest-django and pytest-cov.                                                                                     |
| D3.8 | A — drf-spectacular and drf-spectacular-sidecar.                                                                                    |
| D3.9 | A — Ruff security rules; specialized scanners deferred.                                                                             |
| D4.1 | A — Traditional Django repository layout.                                                                                           |
| D4.2 | A — Flat domains under apps/.                                                                                                       |
| D4.3 | A — File-first organization; split when justified.                                                                                  |
| D4.4 | B — Pragmatic services for meaningful workflows.                                                                                    |
| D4.5 | B — Base, development, testing and production settings.                                                                             |
| D4.6 | C — Application-local tests plus repository-level integration and acceptance tests.                                                 |
| D4.7 | A — Extract shared code on demand.                                                                                                  |
| D5.1 | Custom — 69-character lines, single quotes, four-space indentation, automatic import sorting and formatter-managed trailing commas. |
| D5.2 | Custom — One task per function, maximum 14 lines per function and 400 lines per file; discuss exceptions.                           |
| D5.3 | A — Standard Python and Django naming.                                                                                              |
| D5.4 | B — Meaningful type annotations on function interfaces.                                                                             |
| D5.5 | A — Minimal, intention-oriented comments and documentation.                                                                         |
| D5.6 | B — Pragmatic testing during each milestone; PostgreSQL for database-dependent tests.                                               |
| D5.7 | A — Minimum 95% test coverage.                                                                                                      |
| D5.8 | B — Local quality verification and GitHub Actions.                                                                                  |
| D5.9 | B — Human-led design and scoped AI-assisted engineering.                                                                            |

## Open implementation details

Exact dependency versions and compatibility, Docker configuration, environment variables and secrets, HTTP API conventions, line-counting rules, and whether the coverage threshold applies to lines or branches remain unresolved. No repository or implementation has been verified yet.

## Proposed next block

- D6 — Technology versions and dependency policy.
- D7 — Docker and development infrastructure.
- D8 — Environment configuration and secrets.
- D9 — HTTP API conventions.
- D10 — Repository initialization and development workflow.
