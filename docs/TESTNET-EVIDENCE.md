# Testnet evidence register

**Last consolidated audit:** 2026-11-08  
**Network:** Stellar Testnet  
**Evidence policy:** historical links and reported E2E results are not represented as freshly re-executed verification.

## Evidence status vocabulary

- **IMPLEMENTED:** code/configuration exists. This does not prove it works.
- **TESTED:** a local/unit/integration test was executed. Record command, commit, and result.
- **REPORTED ON TESTNET:** a transaction/E2E was reported and a transaction URL is available, but was not independently rechecked in this audit.
- **VERIFIED ON TESTNET:** the transaction is confirmed on the named network and the expected contract state/result has been independently inspected or reproduced.
- **PENDING:** missing evidence, unresolved blocker, or unverified behavior.

## ¿SÍ O NEL?

Contract: `CDOIAYBUTI2MQEUC6CJJYCIRPVKJDLVDIN56MU3ALMXO7IRRQNV2ACYT`

| Action | Transaction |
|---|---|
| Initialize | [18414148b1d393f1f77bf3595e92458250b97e54a138ee556d16ac3567348171](https://stellar.expert/explorer/testnet/tx/18414148b1d393f1f77bf3595e92458250b97e54a138ee556d16ac3567348171) |
| Create prediction | [25623df569cc8e378507336d7ac69a77893046d3da9f59f25b31017eb3c81df0](https://stellar.expert/explorer/testnet/tx/25623df569cc8e378507336d7ac69a77893046d3da9f59f25b31017eb3c81df0) |

Recorded observation: create flow for prediction ID 0 and `get_count == 1` were documented. This is not a complete lifecycle proof.

**Outstanding:** independently execute a two-wallet lifecycle: create → participate → close at/after `closes_at` → resolve with authorized resolver → inspect evidence and both wallets' statistics. Audit resolver rotation: the prior code path compared a global resolver with a per-prediction snapshot, potentially stranding pending predictions after rotation.

## TÓMBOLA

Contract: `CAWSHHKO53IQN2YPQLFHG5YODLI7HYC2POTH6XKX37XJWEVT35WRDBOF`

| Action | Transaction |
|---|---|
| VRF request | [5d1a2269ceeab4d4f8e7bd6bfb1326e0c16e533a5c6fa2b52a137539629a8250](https://stellar.expert/explorer/testnet/tx/5d1a2269ceeab4d4f8e7bd6bfb1326e0c16e533a5c6fa2b52a137539629a8250) |
| VRF fulfill | [b0ddcd186677eff98737b0c8283995b9542135e511f1cc7ba43e562b278a4bf2](https://stellar.expert/explorer/testnet/tx/b0ddcd186677eff98737b0c8283995b9542135e511f1cc7ba43e562b278a4bf2) |

Reported observation: raffle reached `Drawn`; report recorded request ID 6, drand round 33743971, and a reproducible winner. Treat as **reported E2E**, not fresh independent verification.

**Critical outstanding:**
- Ensure request and fulfillment use the provider snapshot stored on the raffle, not a mutable global provider.
- Remove the final biased modulo fallback in rejection sampling. Never fall back to `% n` after bounded rejection attempts.
- Recheck the deployed provider contract, verification keys, drand chain/round, request binding, and current oracle configuration.
- Publish a reproducible verification procedure and trust model.

## BANDERA ROJA

Contract: `CA53OBINI3BRK22ZWN2CDGB4Q7QPNW5MH74ZLSHIBIQ35KF5RWBEBOR`

| Action | Transaction |
|---|---|
| Create poll | [6830b034344027d0b9a4600be2fa6d231c5a16464a96b2f36978ebf29cc74ca7](https://stellar.expert/explorer/testnet/tx/6830b034344027d0b9a4600be2fa6d231c5a16464a96b2f36978ebf29cc74ca7) |
| Publish result | [1136f3e6d8d7d651f829d66cbc71c6a3fdea24d618ad0cb788d5510e19305510](https://stellar.expert/explorer/testnet/tx/1136f3e6d8d7d651f829d66cbc71c6a3fdea24d618ad0cb788d5510e19305510) |

Reported observation: poll 2 resolved with winning option 1, total votes 2, counts `[0,2]`, and a reproducible result hash.

**Critical outstanding:** inspect persistent stats after resolution. The latest audit found that individual score calculation did not establish that aggregate `Stats.points` and `Stats.correct` were persisted for each predictor. A ranking UI must not imply a complete leaderboard until this is fixed and verified with multiple wallets.

## Verification record template

For every new evidence item, add:

```text
Date/time (UTC):
Project:
Network:
Contract ID:
Contract WASM hash:
Action:
Transaction hash:
Transaction status:
Source account:
Relevant contract state before:
Relevant contract state after:
Independent reproduction steps:
Explorer/RPC links:
Commit:
Reviewer:
Limitations:
```

A transaction hash proves neither the full product flow nor the correctness of off-chain evidence. Record the state read after confirmation.
