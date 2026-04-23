# ADR-0005: Shopify app scaffolding fallback (official template clone)

## Status

Accepted

## Context

Shopify CLI scaffolding can be blocked by:

- org/account permission issues
- interactive prompts in non-interactive environments

We still needed a modern Remix Shopify app baseline in-repo quickly.

## Decision

If CLI scaffolding is blocked, scaffold by **cloning the official Shopify Remix app template** into the target app directory (`sniper-plugin/`), then wire it into the umbrella’s Docker/E2E conventions.

## Consequences

- Partner Dashboard linking (`shopify.app.toml` `client_id`, etc.) may still need follow-up via Shopify CLI or manual configuration.
- We treat “template in repo + docker smoke” as the baseline integration bar until Partner linkage is complete.
