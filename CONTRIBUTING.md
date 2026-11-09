# Contributing to STB Suite

Thanks for helping improve the STB Suite documentation hub.

## Where changes belong

- Product code, frontend behavior, smart contracts, tests, and deployment configuration belong in each game's source repository.
- Cross-game architecture, contract registry, evidence index, release status, and suite-level guidance belong here.
- Do not copy private source code or secrets into this public repository.

## Documentation changes

When updating a contract or release record, include the evidence needed to reproduce the claim:

- project and network;
- contract ID;
- exact source commit;
- transaction hash and explorer URL;
- observed transaction status;
- relevant contract state before and after;
- verification method and date/time in UTC;
- limitations or unverified assumptions.

Use the status vocabulary in [docs/TESTNET-EVIDENCE.md](docs/TESTNET-EVIDENCE.md). Do not promote a reported transaction to independently verified without rechecking the ledger and expected contract state.

## Quality bar

- Prefer precise, falsifiable statements over marketing claims.
- Never publish secrets, private keys, seeds, mnemonics, or recovery material.
- Do not invent demo URLs, test results, contract metadata, or user metrics.
- Keep Testnet and Mainnet status explicit.
- Distinguish votes, predictions, results, and scores.
- Document oracle and randomness trust assumptions.

## Pull requests

Keep changes focused. Explain what changed, why it changed, and how claims were verified. Include links to source commits and Testnet evidence where applicable.
