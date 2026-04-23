# Primary Instructions (Shopify AI Umbrella)

## Always read this first

Before starting any new sub-project in this monorepo, **always read this file first** and follow it.

## Repo layout

- Root: `~/Dev/ShopifyAI_Umbrella`
- First app: `sniper-plugin/` (Shopify Remix app template)

## Docker patterns (standard)

Use the repo-root `docker-compose.yml` as the single source of truth for local infra and test running:

- **App**: `sniper-plugin` service
- **State**: `postgres` + `redis`
- **E2E**: `e2e` service (Playwright)

### E2E command

Run E2E via Docker (preferred):

```bash
docker compose run --rm e2e
```

Or via npm helper:

```bash
npm run e2e:docker
```

## Cursor / PR guardrail

This repository uses `.cursor/rules.json`.

**Before any PR is created**, the agent MUST:

1. Run the Docker E2E suite: `docker compose run --rm e2e`
2. If it fails, the agent is authorized to self-correct and re-run until it passes.

## Git hygiene (non-negotiable)

- **Never commit `node_modules/`**
- Keep secrets out of git:
  - Don’t commit `.env` files
  - Use local env files or secret managers

## Shopify scaffolding note

If Shopify CLI scaffolding fails due to org/permissions, prefer:

- cloning the official Shopify app template into the target app directory, then
- wiring the repo-level docker + E2E patterns as above.

