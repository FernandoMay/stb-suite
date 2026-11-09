# Roadmap

Priorities below reflect the consolidated audit of 8 Nov 2026. Revalidate before treating them as current.

## P0 — Contract correctness

1. **TÓMBOLA:** use the provider stored on each raffle for request and fulfillment; eliminate biased modulo fallback; test provider rotation and invalid/replayed proof paths.
2. **BANDERA ROJA:** persist aggregate points/correct counts for every predictor on resolution; prove with multiple wallets and post-resolution reads.
3. **¿SÍ O NEL?:** make resolver rotation safe for pending predictions; define and test migration/authorization semantics.

## P1 — Reproducible E2E

1. Run current Rust contract tests and frontend tests on the exact audited commits.
2. ¿SÍ O NEL?: two-wallet create/participate/close/resolve/stats E2E.
3. TÓMBOLA: independent verification of current oracle deployment, cryptographic proof, drand round, provider configuration, and winner derivation.
4. BANDERA ROJA: multiple predictors, result publication, persisted stats, and ranking reconciliation.

## P1 — Frontend and operations

- Verify active wallet network before every write.
- Require non-empty actual transaction hash.
- Re-read state after confirmation.
- Surface RPC/indexing errors instead of silently skipping records.
- Verify all three production deployments and environment variables.
- Reconcile stale README deployment IDs, WASM hashes, and old mock descriptions.

## P2 — Suite polish

- Publish a central landing page linking the three live apps.
- Add a common evidence format and release checklist.
- Add CI for Rust tests, frontend tests, lint, and production builds.
- Add per-game status badges only when backed by reproducible CI or evidence.
