# Architecture Decision Records (ADRs)

This folder records **durable decisions** for the `shopify-ai-umbrella` monorepo.

## Index

- [ADR-0001: Monorepo layout + “read first” instructions](./0001-monorepo-layout-and-primary-instructions.md)
- [ADR-0002: Docker Compose as the local integration surface](./0002-docker-compose-integration-surface.md)
- [ADR-0003: Playwright E2E in Docker + PR gate](./0003-playwright-e2e-docker-and-pr-gate.md)
- [ADR-0004: Postgres for Prisma session storage](./0004-postgres-for-prisma-session-storage.md)
- [ADR-0005: Shopify app scaffolding fallback (template clone)](./0005-shopify-app-scaffold-fallback-template-clone.md)
- [ADR-0006: Remove committed `node_modules` from git history](./0006-remove-node-modules-from-git-history.md)

## How to add a new ADR

1. Copy the nearest ADR as a template.
2. Use the next number: `0007-...md`.
3. Keep it short: **Context → Decision → Consequences → Status**.
