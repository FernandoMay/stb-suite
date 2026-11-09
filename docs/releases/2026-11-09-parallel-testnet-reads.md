# Release record — Parallel Testnet reads and honest loading states

**Date:** 2026-11-09  
**Scope:** ¿SÍ O NEL?, BANDERA ROJA, and TÓMBOLA  
**Network:** Stellar Soroban Testnet

## Summary

The project owner reports that all three applications were updated, pushed, built, tested, and checked live with screenshots. The change parallelizes contract reads used to populate enumerations and makes loading/error states explicit instead of presenting temporary empty values as real Testnet data.

## Source commits

| Application | Commit |
|---|---|
| ¿SÍ O NEL? | `79f2c7e` |
| BANDERA ROJA | `940e1fb` |
| TÓMBOLA | `2566139` |

These are the short commit identifiers supplied in the release report. Full commit SHAs and deployed-commit correspondence have not been independently checked in this hub update.

## Changes reported

- Contract reads for each enumeration now run concurrently through `Promise.all` (the count read and the per-ID reads).
- Per-ID failures remain isolated: an unreadable record resolves to `null` and is filtered by the expected type instead of failing the entire listing.
- The list uses a single explicit loading state, **“Consultando Testnet…”**, until the first read batch completes.
- ¿SÍ O NEL?: removed misleading zero counters and “sin pregunta en juego” during loading; displays a hero skeleton and “Leyendo pregunta…”, hides stats until data arrives, and surfaces RPC errors.
- BANDERA ROJA: displays `…` for counters while loading rather than false zeroes; removed generic “BR” lettering from the flag SVG.
- TÓMBOLA: restored the official garrafón asset that had been missing because the placeholder file was not a served image; VRF bar and draw pill display `…` while loading.

## Validation reported by project owner

| Check | Reported result | Evidence status in this hub |
|---|---|---|
| `npm test` — ¿SÍ O NEL? | PASS | Owner-reported; logs not attached here |
| `npm run build` — ¿SÍ O NEL? | PASS | Owner-reported; logs not attached here |
| `npm test` — BANDERA ROJA | PASS | Owner-reported; logs not attached here |
| `npm run build` — BANDERA ROJA | PASS | Owner-reported; logs not attached here |
| `npm test` — TÓMBOLA | PASS | Owner-reported; logs not attached here |
| `npm run build` — TÓMBOLA | PASS | Owner-reported; logs not attached here |
| Live UI checked with screenshots on all three sites | PASS, per owner | Screenshots were reported but are not attached to this record |
| First batch typically resolves in about 4–6 seconds | Observed, per owner | Not an independently measured benchmark |

## Remaining verification

This release record does **not** close the previously documented contract/security audit findings. The following checks remain recommended before treating this as an independently audited release:

1. Match each deployed site's build to the exact source commit above.
2. Retain screenshots and/or browser traces showing actual Testnet responses rather than fixtures.
3. Exercise an RPC failure and a single corrupted/unreadable ID; confirm the rest of the list still renders and the error is accurately surfaced.
4. Exercise a count change while the concurrent enumeration is in flight; define and verify the expected consistency behavior (for example, snapshot/retry or graceful omission).
5. Re-run the exact test suites and builds from clean installs, retaining command output and environment details.

## Status interpretation

- **Implemented:** parallel reads and explicit loading/error presentation, as reported by the project owner.
- **Tested:** local test suites and production builds reported passing by the project owner.
- **Live-checked:** all three sites reportedly inspected with screenshots by the project owner.
- **Independently verified in this hub update:** repository metadata and documentation changes only. No source checkout, deployment SHA comparison, browser session, or live RPC replay was performed for this record.

This update improves perceived responsiveness and prevents transient loading state from being misrepresented as real zero-valued Testnet data. It does not by itself prove full contract lifecycle correctness or resolve previously recorded security findings.
