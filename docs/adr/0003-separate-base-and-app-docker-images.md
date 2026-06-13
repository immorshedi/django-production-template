# 0003 - Separate Docker images into base and app layers

## Status
Accepted

## Context
Python dependencies usually change less frequently than application source code.

In a single Docker image build, any source code change can invalidate dependency-related layers, which slows down builds and reduces cache efficiency. This is especially noticeable in CI/CD pipelines and iterative local development.

This template aims to improve:
- Docker build speed
- image layer reuse
- dependency caching
- clarity of responsibilities inside container builds

## Decision
Use two Docker image responsibilities:

- a `base` image for:
  - Python runtime
  - system packages
  - `uv`
  - Python dependencies from dependency definition files

- an `app` image for:
  - project source code
  - runtime command configuration

The application image is built on top of the reusable base image.

## Consequences

### Positive
- faster rebuilds when only source code changes
- better Docker cache utilization
- clearer separation between dependencies and application code
- easier reuse across environments and pipelines
- more efficient CI/CD workflows

### Negative
- slightly more complex image management
- base image versioning must be handled carefully
- documentation and CI/CD configuration become more detailed

## CI/CD Implications
This separation also makes it possible to write CI rules in both GitLab CI and GitHub Actions to avoid unnecessary base image build jobs.

For example, the base image job should run only when files such as these change:
- base Dockerfile files
- dependency definition files such as `pyproject.toml`, `uv.lock`, or `requirements*.txt`

This helps prevent rebuilding the base image when only application source code changes.

## Notes
This decision supports production-oriented workflows where build performance, reproducibility, and pipeline efficiency matter.