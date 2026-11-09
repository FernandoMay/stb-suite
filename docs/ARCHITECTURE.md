# Architecture

## System boundaries

STB Suite is a documentation and discovery hub. It is not a shared runtime, wallet, backend, or cross-game smart contract.

Each game owns:
- its frontend and deployment;
- its Soroban contract and storage model;
- its wallet integration;
- its transaction lifecycle and error handling;
- its tests, deployment scripts, and release process.

## Common transaction lifecycle

Every state-changing UI action should follow:

1. Validate configuration and require the intended network (Testnet).
2. Connect the user's wallet and verify its active address/network.
3. Build the Soroban invocation using the correct contract and arguments.
4. Simulate/prepare as required by the Stellar SDK.
5. Request wallet authorization/signature.
6. Submit the signed transaction.
7. Wait for final network confirmation; handle timeout and failed status distinctly.
8. Extract and display the actual transaction hash.
9. Read the affected contract state again.
10. Display success only if the confirmed state matches the expected transition.

A wallet popup closing is not transaction confirmation. A successful RPC submission is not necessarily final confirmation. A locally computed identifier is not a transaction hash.

## Game-specific boundaries

### ¿SÍ O NEL?

- Prediction lifecycle and participation are Soroban state.
- Resolver authorization is contract-enforced.
- Evidence hash anchors a reference; the evidence artifact itself needs a separate availability/provenance process.
- Reputation/ranking must be read from contract state.

### TÓMBOLA

- Entry set must be frozen before requesting randomness.
- Randomness request must be bound to the raffle ID, provider, request ID, and intended draw.
- Fulfillment must validate the expected provider and cryptographic proof.
- Winner derivation must be deterministic and unbiased under the documented algorithm.
- No local PRNG or predictable substitute may be used in runtime.

### BANDERA ROJA

- Vote and prediction are separate concepts and flows.
- If votes are on-chain and public, state that wallet-to-choice association is visible.
- If votes are off-chain, describe their signature, storage, and verification model; do not imply Soroban stores them.
- Prediction, result publication, scoring, and ranking need separately defined state transitions.

## Shared frontend requirements

- Explicit network indicator and active wallet address.
- Block writes on wrong network or missing contract configuration.
- Clear states: awaiting signature, submitted, confirming, confirmed, rejected, failed, timed out.
- Preserve transaction hash and explorer link after confirmation.
- Read-after-write for the relevant entity and user stats.
- Surface partial read/indexing failures; do not silently present incomplete results as complete.
- Pagination/indexing must not assume a small fixed maximum record count.
