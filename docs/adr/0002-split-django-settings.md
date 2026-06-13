# 0002 - Split Django settings into environment-specific modules

## Status
Accepted

## Context
A single `settings.py` file becomes harder to maintain as a Django project grows.

This template needs clear separation between:
- shared settings
- local development settings
- production settings
- test settings

Keeping all configuration in one file increases the risk of:
- enabling `DEBUG` in production
- mixing local and production concerns
- making tests depend on development configuration
- reducing clarity for contributors

## Decision
Split Django settings into multiple modules:

- `base.py` for shared settings
- `local.py` for local development
- `production.py` for production configuration
- `test.py` for test-specific configuration

The Django settings module will be selected explicitly through `DJANGO_SETTINGS_MODULE`, with safe defaults depending on the entrypoint.

## Consequences

### Positive
- clearer separation of responsibilities
- safer production defaults
- easier testing and future configuration changes
- better readability for contributors
- easier documentation of environment-specific behavior

### Negative
- more files to maintain
- possible duplication if settings are not organized carefully
- developers must understand which settings module is active

## Notes
This decision keeps environment concerns explicit and prepares the project for future improvements such as environment variable based configuration and deployment-specific security settings.