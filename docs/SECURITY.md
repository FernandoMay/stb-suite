# Security and trust assumptions

## General

- Testnet only. Never request, store, or commit private keys, seeds, mnemonics, or wallet recovery material.
- No mock/simulated state in production runtime.
- Tests may use mocked authorization and local ledger environments, but test fixtures must remain isolated from production builds.
- No fake hashes, fabricated user counts, synthetic transactions, or success states before confirmation.
- Use least-privilege contract roles and document admin/resolver rotation.
- Treat RPC, Horizon, wallet providers, deployment environment variables, and external oracles as dependencies that can fail or be compromised.

## ¿SÍ O NEL?

Threats:
- resolver compromise, censorship, incorrect result, or key rotation;
- evidence hash supplied without accessible/authentic evidence;
- close/resolution authorization mismatch;
- ranking based on stale or incomplete reads.

Required controls:
- resolver authorization tied to a clearly defined lifecycle and migration policy;
- immutable audit trail of evidence references;
- read-after-write and independent state inspection;
- documented dispute/correction policy.

## TÓMBOLA

Randomness is a critical security property.

**Not acceptable as randomness:** `Math.random`, timestamp, ledger sequence, organizer-selected seed, transaction hash, block/ledger metadata, user-provided seed, or any equivalent predictable/controllable value.

Required controls:
- cryptographic proof verification with a documented trust root;
- request binding to raffle ID and frozen participant set;
- provider snapshot semantics and safe provider rotation;
- domain-separated deterministic winner derivation;
- unbiased bounded-integer mapping; no biased modulo fallback;
- explicit liveness/failure behavior (a failed oracle must not silently produce a winner);
- independent reproduction from published proof and participants.

A VRF/oracle solution may still have operator, key-management, censorship, and availability assumptions. Disclose them.

## BANDERA ROJA

Threats:
- vote/prediction semantic confusion;
- resolver manipulation or ambiguous tie rules;
- scoring not persisted even though a per-user calculation returns a value;
- public wallet-linked votes being misrepresented as anonymous.

Required controls:
- explicit vote and prediction data models;
- deterministic result derivation or documented resolver authority;
- persistent points/correct counters updated exactly once;
- tests with multiple wallets and post-resolution stats reads;
- privacy statements matching actual storage and visibility.

## Disclosure

Do not call a system “trustless,” “fully decentralized,” “anonymous,” “provably fair,” or “cryptographically verified” unless the implementation and independent evidence support the exact claim.
