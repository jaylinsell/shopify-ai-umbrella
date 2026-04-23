# ADR-0002: Docker Compose as the local integration surface

## Status

Accepted

## Context

We want a repeatable local environment that includes:

- the Shopify app container
- backing services (Postgres/Redis)
- a headless E2E runner

…and we want CI-like behavior locally without relying on each developer’s bespoke setup.

## Decision

Use **repo-root** `docker-compose.yml` as the single integration surface for:

- `postgres` (state)
- `redis` (state)
- `sniper-plugin` (app)
- `e2e` (Playwright)

## Consequences

- Local workflows should prefer `docker compose ...` over “install everything globally”.
- App-specific Docker details should remain in `sniper-plugin/Dockerfile`, but orchestration stays at the repo root.
