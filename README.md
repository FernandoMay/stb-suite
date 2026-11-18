# STB Suite

**Three on-chain games. One verifiable Stellar experience.**

STB Suite is a portfolio of three independent, wallet-connected games built on **Stellar Soroban Testnet**:

1. **¿SÍ O NEL?** — social predictions and on-chain reputation.
2. **TÓMBOLA** — transparent raffles designed around verifiable randomness.
3. **BANDERA ROJA** — collective polls, separate predictions, and reputation.

This repository is the public-facing hub for the suite. The applications and smart contracts remain in their own repositories; this hub centralizes product documentation, links, contract identifiers, verification evidence, architecture, security assumptions, and release status.

> **Network status:** Stellar Testnet only. These projects are not Mainnet products and must not be represented as such.

## Projects

| Game | Purpose | Source repository | Contract |
|---|---|---|---|
| ¿SÍ O NEL? | Prediction game | [FernandoMay/si-o-nel](https://github.com/FernandoMay/si-o-nel) *(private)* | `CDOIAYBUTI2MQEUC6CJJYCIRPVKJDLVDIN56MU3ALMXO7IRRQNV2ACYT` |
| TÓMBOLA | Raffle / draw | [FernandoMay/tombola](https://github.com/FernandoMay/tombola) *(private)* | `CAWSHHKO53IQN2YPQLFHG5YODLI7HYC2POTH6XKX37XJWEVT35WRDBOF` |
| BANDERA ROJA | Polls + predictions | [FernandoMay/bandera-roja](https://github.com/FernandoMay/bandera-roja) *(private)* | `CA53OBINI3BRK22ZWN2CDGB4Q7QPNW5MH74ZLSHIBIQ35KF5RWBEBOR` |

The source repositories are currently private. This public hub documents the suite but does not grant access to their source code.

### Live experiences

Deployment URLs must be confirmed against the current Netlify site configuration before being treated as canonical. Until then, use the deployment information maintained by the project owner; no unverified demo URL is published here.

## Stellar Testnet contracts

All three contract identifiers above are Testnet identifiers. Contract explorers:

- [¿SÍ O NEL? contract](https://stellar.expert/explorer/testnet/contract/CDOIAYBUTI2MQEUC6CJJYCIRPVKJDLVDIN56MU3ALMXO7IRRQNV2ACYT)
- [TÓMBOLA contract](https://stellar.expert/explorer/testnet/contract/CAWSHHKO53IQN2YPQLFHG5YODLI7HYC2POTH6XKX37XJWEVT35WRDBOF)
- [BANDERA ROJA contract](https://stellar.expert/explorer/testnet/contract/CA53OBINI3BRK22ZWN2CDGB4Q7QPNW5MH74ZLSHIBIQ35KF5RWBEBOR)

Transaction evidence is summarized in [Testnet evidence](docs/TESTNET-EVIDENCE.md). Evidence is classified as reported, independently rechecked, or pending. A link alone is not proof that a transaction was independently re-executed during the latest review.

## Product principles

- **No simulated runtime:** no fake transaction hashes, pretend confirmations, or demo-only state presented as live chain state.
- **Wallet authorization:** state-changing operations must be authorized by the relevant wallet or explicitly authorized contract role.
- **Confirmation before success:** the UI must not display success until the network confirms the transaction.
- **Read-after-write:** after confirmation, the application must read the relevant contract state again.
- **Evidence over claims:** contract IDs, network, transaction hash, and verifiable status must accompany claims of on-chain execution.
- **Testnet honesty:** Testnet assets have no Mainnet value; Testnet deployment is not a production/Mainnet launch.
- **Separation of concerns:** voting, prediction, randomness, result resolution, and scoring must not be conflated.

## Architecture at a glance

```text
                         STB SUITE HUB
           Documentation · Evidence · Links · Governance
                              |
             +----------------+----------------+
             |                |                |
          ¿SÍ O NEL?        TÓMBOLA        BANDERA ROJA
          Prediction        Raffle          Poll + prediction
             |                |                |
          Soroban           Soroban          Soroban
          contract          contract         contract
             +----------------+----------------+
                              |
                     Stellar Testnet RPC
                              |
                     Wallet authorization
```

The three apps are separate deployables with separate contracts and product-specific rules. This hub does not aggregate or proxy their transactions.

## Documentation

- [Product overview](docs/PRODUCT-OVERVIEW.md)
- [Architecture](docs/ARCHITECTURE.md)
- [Contract registry](docs/CONTRACT-REGISTRY.md)
- [Testnet evidence](docs/TESTNET-EVIDENCE.md)
- [Security and trust assumptions](docs/SECURITY.md)
- [QA and release gates](docs/QA-RELEASE-GATES.md)
- [Roadmap](docs/ROADMAP.md)
- [Glossary](docs/GLOSSARY.md)

## Latest audit

The 18 Nov 2026 source audit found no functional commits since 9 Nov. The suite-wide unauthenticated initializer remains P0; TÓMBOLA still has a terminal biased modulo fallback and ignores the per-raffle provider snapshot; BANDERA ROJA still has a Testnet contract-ID mismatch and does not persist the scoring fields shown by its Ranking page. No fresh Testnet state, test execution, or Netlify dashboard deployment was independently verified. See [the full audit](docs/audits/2026-11-18.md).

## Latest release record

The 9 Nov 2026 update for parallel Testnet reads and honest loading states is documented in [the release record](docs/releases/2026-11-09-parallel-testnet-reads.md). Build/test results and live screenshot checks are explicitly labeled as project-owner-reported; independent deployment/source verification remains pending.

## Current readiness snapshot

This is a conservative source snapshot from 18 Nov 2026, not a live RPC or deployment query. Tests are present in the repositories but were not run in this audit:

| Game | IMPLEMENTED | TESTEADO | Testnet evidence | PENDIENTE |
|---|---|---|---|---|
| ¿SÍ O NEL? | Prediction lifecycle and persisted per-wallet scoring | Rust/Vitest scripts and contract tests exist; not run in this audit | Historical initialize/create only; full lifecycle not independently rechecked | Unauthenticated initialize; resolver rotation; two-wallet E2E |
| TÓMBOLA | Soroban VRF request/fulfill path; MockVrf is test-only | VRF/rejection tests exist; not run in this audit | 7 Nov E2E recorded by project; not independently rechecked | Unauthenticated initialize; terminal biased modulo fallback; global verifier instead of per-raffle snapshot; oracle/WASM proof revalidation |
| BANDERA ROJA | Separate public on-chain votes and on-chain predictions; result derived from counts | Rust/Vitest tests exist; not run in this audit | Historical poll creation/result only; not independently rechecked | Unauthenticated initialize; wrong contract ID in Netlify/README; persistent correct/points scoring |

**Do not interpret “Testnet evidence” as “all product flows independently verified.”** Detailed caveats and transaction links are in [TESTNET-EVIDENCE.md](docs/TESTNET-EVIDENCE.md).

## Contributing

Changes to a game belong in its source repository. This hub should be updated when any of the following changes:

- contract ID, WASM hash, deployment, or network;
- transaction evidence or independently reproduced E2E;
- canonical demo or website URL;
- security assumptions, oracle configuration, or authorization rules;
- release stage or critical blockers.

Every evidence update should include date/time (UTC), network, contract ID, transaction hash, action, observed result, and verification method. See [QA and release gates](docs/QA-RELEASE-GATES.md).

## License

No license is granted by this hub unless a `LICENSE` file is added. The source repositories retain their own licensing terms. Do not assume that public visibility alone grants reuse rights.
