# Engineering instructions

## Principles and architecture

- Favor simplicity, performance, clean code, reusability, maintainability,
  scalability, readability, security and testability. Prefer explicit,
  understandable and composable solutions; avoid premature abstractions
  and unnecessary complexity. Extract reuse when justified and measure
  before optimizing.
- Build an evolutionary modular monolith using Python, Django and Django
  REST Framework, with PostgreSQL, Redis and Django RQ.
- Use flat domain applications under `apps/` and file-first organization;
  split modules when justified. Use pragmatic services for meaningful
  business workflows and `common/` for shared infrastructure when justified.
  Keep domain business logic in its owning domain.
- Keep tests local to applications; place integration and acceptance tests
  at repository level.

## Code conventions

- Use a maximum Python line length of 69 characters, single quotes and
  four-space indentation. Sort imports automatically and let the formatter
  manage trailing commas. Follow standard Python and Django naming.
- Add meaningful type annotations to function interfaces. Keep comments
  and documentation minimal and focused on intent.
- Give each function one coherent responsibility. Limit functions to 14
  substantive lines and files to 400 physical lines. Count implementation
  body lines, including multiline expressions and nested blocks; exclude
  signatures, decorators, blank lines, standalone comments and docstrings.
- Use Ruff for applicable formatting, linting and security checks. Review
  function and file lengths manually. Report justified exceptions; do not
  artificially split coherent code to satisfy numerical limits.

## Dependencies and infrastructure

- Use uv with package-specific bounded dependency ranges, one committed
  `uv.lock` and locked installations. Add dependencies only for justified
  requirements.
- Use Docker-first development with four Compose services: `api`, `worker`,
  `db` and `redis`. API and worker share an application image. Run
  application containers as non-root users and keep their Python environment
  at `/opt/venv`.
- Apply database migrations explicitly, never automatically during
  application startup.

## Testing and verification

- Use pytest, pytest-django and pytest-cov. Implement meaningful tests
  alongside functionality; use PostgreSQL for database-dependent tests and
  isolate development and testing state.
- Enable branch coverage and enforce a global minimum of 95% combined
  statement and branch coverage. Test critical security and business
  behavior independently of coverage percentages.
- Run relevant available checks during each milestone and full applicable
  verification before integration. Never claim an unavailable or unexecuted
  check passed.

## HTTP API

- Use resource-oriented REST with justified domain actions and URL path
  versioning, initially `/api/v1/`. Use lowercase plural collection names,
  kebab-case paths and trailing slashes. Use UUIDv4 identifiers for
  independently identifiable domain resources.
- Use snake_case JSON properties, UTC timestamps and explicit duration units.
  Follow standard HTTP semantics and return successful resource
  representations directly.
- Use a unified error envelope containing errors with `code`, `field` and
  `detail`. Use JSON Pointer paths for fields and null for non-field errors.
- Default to cursor pagination, with justified exceptions; use a default
  page size of 20 and a maximum of 100.
- Validate requests strictly: reject unknown fields, read-only input fields
  and empty PATCH requests. Accept valid unchanged PATCH requests without
  unnecessary state changes. Generate and validate OpenAPI documentation.

## Security

- Use secure defaults and explicit authorization boundaries. Deny
  unauthenticated domain API access by default; public endpoint exceptions
  must be intentional.
- Never commit credentials, secrets or authentication tokens, or log
  sensitive information. Use environment-based configuration and fail fast
  for missing or invalid critical configuration.
- Knox is the selected client authentication technology; its implementation
  belongs to the Users domain. Establish the custom user model before initial
  database migrations.

## Development and AI collaboration

- Follow Explore → Decide → Define → Implement → Review → Verify → Learn →
  Commit. Keep architectural decisions human-led and milestones small and
  explicitly scoped.
- Use `main` as the permanent integration branch, lightweight purpose-based
  feature branches, Conventional Commits and fast-forward-only integration.
  Once CI is operational, verify locally and remotely before integration.
- Do not commit, push, merge, tag or change branches without explicit user
  authorization.
- Inspect relevant repository files and instructions before implementation.
  Follow the approved milestone scope and do not silently change accepted
  architectural decisions. Ask for clarification when requirements conflict
  or significant decisions are missing.
- Avoid unrelated refactoring and speculative features; preserve user changes.
  Report assumptions, deviations, limitations and unresolved issues. Keep
  relevant documentation synchronized with implementation. Treat approved
  decision registers and foundation contracts as authoritative when available.
