# Inusai API 2.0 --- F0 Roadmap

**Date:** 2026-11-26\
**Status:** F0.1 approved; F0.2--F0.9 pending.

Authority: Decision Registers 01--03 and Foundation Contract 01. Milestones are sequential checkpoints, not software release versions. No implementation or Codex prompts are included.

Milestone Scope Status

---

F0.1 Foundation contract and compatibility Design complete
F0.2 Repository and engineering documentation Next
F0.3 Python and dependencies Pending
F0.4 Docker infrastructure Pending
F0.5 Django settings and minimal identity Pending
F0.6 Quality engineering Pending
F0.7 Common HTTP infrastructure Pending
F0.8 GitHub Actions Pending
F0.9 Acceptance and integration Pending

## F0.1 --- Foundation contract

Deliverables: 38 foundation decisions, consolidated contract, roadmap. Candidate stack selected; actual dependency and runtime verification explicitly deferred to implementation. No repository changes.

## F0.2 --- Repository initialization

Create empty public GitHub repository without explicit license; initialize locally, establish main and purpose-based foundation branch. Prepare README, AGENTS.md, ignore rules and evolutionary documentation. Verify remote, branch state, documentation and absence of secrets. Confirm legacy archive handling before changing legacy repositories.

## F0.3 --- Python project and dependency management

Define Python 3.14 support, pyproject.toml, bounded package-specific ranges, runtime and dev group, pinned uv tooling and uv.lock. Verify official release/support metadata, exact package versions, resolution and locked install. Report incompatibilities for explicit approval. Knox deferred to Users.

## F0.4 --- Docker development infrastructure

Verify official image tags, build shared non-root app image, configure compose.dev.yml with api/worker/db/redis, /app bind mount, /opt/venv, volumes, health checks, localhost port and Redis AOF/noeviction. Establish environment example and URL injection. Verify image build, permissions, network and persistence. Application service startup verification may require F0.5; do not claim full startup before Django exists. No automatic migrations.

## F0.5 --- Django foundation

Create Django project and four settings modules, configuration validation, logging, secure production baseline, PostgreSQL and Redis/RQ integration. Implement minimal custom user model and manager; configure AUTH_USER_MODEL before initial migrations. Verify normalization, uniqueness, inactive default, active superuser, explicit migrations, Django checks, connectivity and worker execution. No Knox or account workflows.

## F0.6 --- Quality engineering

Configure Ruff, pytest, pytest-django and pytest-cov; isolated PostgreSQL and Redis test state, coverage scope and combined 95% threshold. Verify formatting/linting, meaningful infrastructure and identity tests, test isolation and coverage. Review length limits and justified exceptions. Testing occurs throughout all milestones, not only here.

## F0.7 --- Common HTTP infrastructure

Implement focused common/api package, URL versioning, unified errors with JSON Pointer paths, cursor pagination, strict validation, restrictive permission defaults, operational health endpoints and development/testing OpenAPI with local assets. Verify behavior and schema, production docs disabled, no premature domain endpoints. Use test-only fixtures/endpoints where necessary to verify generic contracts (proposed implementation technique, not a new domain requirement).

## F0.8 --- Continuous integration

GitHub Actions separate quality, testing and schema jobs; locked installations, compatible PostgreSQL/Redis and fresh disposable state. Verify all jobs remotely, progressive branch protection and documented local/remote verification workflow. Mandatory PRs deferred.

## F0.9 --- Foundation acceptance and integration

- [ ] Fresh clone and reproducible locked installation.
- [ ] All four Compose services operational.
- [ ] PostgreSQL and Redis connectivity verified.
- [ ] Custom user model and explicit initial migrations verified.
- [ ] Background job execution verified.
- [ ] Environment validation and production settings verified.
- [ ] HTTP errors, pagination, validation and health endpoints tested.
- [ ] OpenAPI generated and validated.
- [ ] Ruff formatting and linting successful.
- [ ] All tests passing, combined coverage \>=95%.
- [ ] GitHub Actions successful.
- [ ] README and AGENTS.md reviewed.
- [ ] No committed secrets or unresolved critical defects.
- [ ] Full applicable verification and human approval before fast-forward integration to main.

## Next phase --- Users domain

Design and verify Knox compatibility, then implement client authentication, sessions and account lifecycle incrementally. Do not automatically inherit Generation 1 contracts. Production deployment and remaining product domains are deferred.

## Workflow for each milestone

Explore, decide, specify, implement, review, verify, learn, commit. Prepare scoped Codex tasks only after the corresponding implementation contract is approved. Report deviations, limitations and verification evidence. No milestone is complete merely because code was generated.
