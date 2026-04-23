# ADR-0003: Playwright E2E in Docker + PR gate

## Status

Accepted

## Context

We need a minimal automated check that the app boots and serves traffic in the composed environment, and we want agents to run the same check before proposing PRs.

## Decision

- Add Playwright tests at repo root (`playwright.config.ts`, `tests/e2e/`).
- Run them via the `e2e` service in `docker compose`.
- Add `.cursor/rules.json` requiring:

`docker compose run --rm e2e`

before PR creation, with permission to self-correct until green.

### Implementation notes (accepted tradeoffs)

- The `e2e` container bind-mounts the repo at `/work` **and** uses a named volume for `/work/node_modules` to avoid macOS bind-mount issues during `npm ci`.

## Consequences

- “Green” means **Docker E2E passes**, not “works on my machine only”.
- Smoke tests should remain fast and stable; deeper Shopify OAuth flows belong in dedicated tests later.
