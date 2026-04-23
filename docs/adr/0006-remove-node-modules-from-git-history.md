# ADR-0006: Remove committed `node_modules` from git history

## Status

Accepted

## Context

`node_modules/` was accidentally committed during early scaffolding. Removing it from HEAD is not sufficient if we want a clean clone history and reasonable repo size.

## Decision

Rewrite git history to remove `node_modules/` entirely using `git-filter-repo`, then **force-push** `main` (and preserve a backup branch pointer where helpful).

## Consequences

- Anyone with an old clone must reset to the rewritten `main`.
- We enforce `.gitignore` rules and treat committing `node_modules/` as a repo incident (never acceptable).
