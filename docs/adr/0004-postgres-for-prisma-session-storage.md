# ADR-0004: Postgres for Prisma session storage

## Status

Accepted

## Context

The Shopify Remix template defaulted Prisma to SQLite for local development. For umbrella-level infra consistency (and closer-to-prod local integration), we want the app’s Prisma datasource to align with the Dockerized Postgres service.

## Decision

- Configure Prisma datasource to **PostgreSQL** using `DATABASE_URL`.
- Store migrations under `sniper-plugin/prisma/migrations/`.
- Run `prisma migrate deploy` as part of container startup (`npm run docker-start`).

## Consequences

- Local DB resets are done by wiping Docker volumes (`docker compose down -v`), not deleting a sqlite file.
- Future schema changes require Prisma migrations committed alongside code.
