# ADR-0001: Monorepo layout + “read first” instructions

## Status

Accepted

## Context

We expect multiple Shopify-related apps under one umbrella repository. Future contributors (and agents) need a consistent entry point so they don’t re-derive setup from chat history.

## Decision

- Use a **single monorepo root** at `~/Dev/ShopifyAI_Umbrella`.
- Keep the first app under `sniper-plugin/`.
- Maintain a root-level `primary_instructions.md` that must be read **before** starting a new sub-project.

## Consequences

- New apps should follow the same patterns documented in `primary_instructions.md` and ADRs.
- Operational guidance lives in `primary_instructions.md`; durable rationale lives in `docs/adr/`.
