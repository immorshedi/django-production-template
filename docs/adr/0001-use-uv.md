# 0001 - Use uv for dependency management

## Status
Accepted

## Context
This repository aims to be a modern, production-oriented Django template.

The project needs:
- fast dependency installation
- reproducible environments
- a lockfile-based workflow
- a clean developer experience for local development and Docker builds

Traditional `pip` + `requirements.txt` works well, but it requires extra tooling or conventions to provide lockfile guarantees and usually results in slower installs.

## Decision
Use `uv` as the primary Python dependency management tool for this repository.

The project will:
- declare dependencies in `pyproject.toml`
- lock dependency versions in `uv.lock`
- install dependencies with `uv sync`
- use `uv` in local development and Docker builds

## Consequences

### Positive
- faster dependency resolution and installation
- reproducible environments through `uv.lock`
- simplified and modern Python workflow
- better fit for Docker layer caching
- fewer moving parts compared to mixed tooling setups

### Negative
- contributors must be familiar with `uv`
- some environments still expect `requirements.txt`
- CI/CD and documentation must explicitly use `uv`

## Notes
This decision is part of making the template production-oriented from the first commit rather than adding tooling later.