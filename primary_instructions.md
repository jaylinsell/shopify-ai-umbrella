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

### Database (Postgres + Prisma)

`sniper-plugin` uses **Prisma with Postgres** for session storage.

- **Compose contract**: `DATABASE_URL` is set for `sniper-plugin` to point at the `postgres` service.
- **Migrations**: `sniper-plugin` runs `prisma migrate deploy` on container start (`npm run docker-start`).

If you need to reset local DB state completely:

```bash
docker compose down -v
docker compose up -d postgres redis sniper-plugin
```

### Local “smoke” env vars (Docker)

The Docker Compose file includes **dummy** Shopify env vars so the app can boot for local smoke/E2E:

- `SHOPIFY_APP_URL`
- `SHOPIFY_API_KEY` / `SHOPIFY_API_SECRET` (dummy values)
- `SCOPES`

These are **not** real production credentials.

### E2E runner details

The `e2e` service bind-mounts the repo at `/work` **but** uses a named volume for `/work/node_modules` to avoid `npm ci` failures caused by macOS bind-mount semantics.

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

