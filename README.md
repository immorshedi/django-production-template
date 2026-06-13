# django-production-template

A production-oriented Django template built incrementally with modern Python tooling and clear architectural decisions.

## Current focus

- Django
- uv
- Modular Django settings
- Docker
- Reusable Docker base/app image strategy

## Goals

- Production-oriented project structure
- Reproducible Python environments
- Fast Docker builds
- Reusable base images
- Clear environment-specific settings
- CI/CD-ready foundation

## Architecture decisions

This repository documents important technical decisions as ADRs:

- [0001 - Use uv for dependency management](docs/adr/0001-use-uv.md)
- [0002 - Split Django settings into environment-specific modules](docs/adr/0002-split-django-settings.md)
- [0003 - Separate Docker images into base and app layers](docs/adr/0003-separate-base-and-app-docker-images.md)

## Project structure

```text
.
├── README.md
├── app
│   ├── config
│   │   ├── asgi.py
│   │   ├── settings
│   │   │   ├── __init__.py
│   │   │   ├── base.py
│   │   │   ├── local.py
│   │   │   ├── production.py
│   │   │   └── test.py
│   │   ├── urls.py
│   │   └── wsgi.py
│   └── manage.py
├── docker
│   ├── app
│   │   └── Dockerfile
│   └── base
│       └── Dockerfile
├── docs
│   └── adr
│       ├── 0001-use-uv.md
│       ├── 0002-split-django-settings.md
│       └── 0003-separate-base-and-app-docker-images.md
├── pyproject.toml
└── uv.lock
````

## Settings Strategy

The project uses modular Django settings:

- `config.settings.base` for shared settings
- `config.settings.local` for local development
- `config.settings.production` for production
- `config.settings.test` for test runs

This keeps environment-specific configuration explicit, isolated, and easier to maintain.

---

## Docker Strategy

The container setup is split into two responsibilities:

### Base Image

Responsible for:

- Python runtime
- System dependencies
- `uv`
- Python package installation

### App Image

Responsible for:

- Project source code
- Application startup commands

This approach improves Docker layer caching and avoids reinstalling dependencies when only application code changes.

---

## Why This Repository Exists

The goal of this repository is not just to start a Django project, but to provide a reusable backend template with production-minded defaults and documented engineering decisions.

Each important step is introduced incrementally and documented to make the reasoning behind architectural choices clear.

---

## Next Steps

Planned additions include:

- [ ] Traefik
- [ ] PostgreSQL
- [ ] Redis
- [ ] CI/CD pipelines
- [ ] Automated testing
- [ ] Linting and formatting
- [ ] Production application server setup 