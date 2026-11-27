# Inusai API

Backend API for Inusai, an intelligent, interactive and extensible
learning platform. Inusai 2.0 aims to provide a foundation that can
evolve with the platform and its learners.

**Think big. Start simple. Build iteratively.**

## Project status

Inusai 2.0 is in the project foundation stage. The initial architecture
and foundation contract have been approved, and repository initialization
is complete. Application implementation and infrastructure are still
planned.

## Engineering philosophy

We favor simple, explicit and composable solutions, with security,
testability and maintainability built in. We make human-led architectural
decisions, deliver small milestones and measure before optimizing.

## Planned technology

The selected stack is Python, Django and Django REST Framework, backed by
PostgreSQL, Redis and Django RQ. The architecture is an evolutionary
modular monolith. Development is planned around uv, Docker and Compose,
with pytest for testing. These technologies are not yet implemented in this
repository.

## Development workflow

Explore, decide and define each scoped milestone before implementation;
review and verify the result, learn from it, and then commit. Work uses
purpose-based branches, Conventional Commits and fast-forward-only
integration into `main`. See [AGENTS.md](AGENTS.md) for engineering and
collaboration conventions.
