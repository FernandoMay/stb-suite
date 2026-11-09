# Glossary

- **Soroban:** Stellar smart-contract platform.
- **Testnet:** Stellar public test network; tokens have no Mainnet value.
- **Contract ID:** deployed smart-contract address/identifier.
- **WASM hash:** hash identifying the compiled contract artifact.
- **Transaction hash:** network-generated identifier for a submitted transaction; must come from the actual confirmed transaction.
- **Read-after-write:** reading contract state after a write transaction confirms.
- **Resolver:** authorized actor that closes the result of a prediction/poll according to contract rules.
- **VRF:** verifiable random function; a cryptographic mechanism for producing randomness with a proof verifiable against a public key.
- **Oracle:** external or on-chain service that supplies data or computation; its trust and availability assumptions must be documented.
- **Provider snapshot:** provider identity/configuration fixed for a particular raffle/request so a later global rotation cannot silently change its verification context.
- **Vote:** expression of preference in a poll.
- **Prediction:** claim about which outcome will win; separate from a vote.
- **Scoring:** persistent accounting of correct/incorrect predictions and points.
