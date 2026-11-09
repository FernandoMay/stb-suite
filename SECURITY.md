# Security policy

STB Suite is currently a Testnet project and this repository is a public documentation hub.

## Reporting a vulnerability

Please do not publish exploit details, private keys, wallet seeds, mnemonics, or sensitive operational configuration in a public issue.

If GitHub private vulnerability reporting is enabled for this repository, use it. Otherwise, contact the repository owner through their GitHub profile and request a private channel for responsible disclosure.

## Scope

Security reports may concern:
- smart-contract authorization, storage, or state-transition flaws;
- randomness, oracle verification, provider rotation, or winner selection;
- wallet signing and transaction confirmation handling;
- frontend exposure of secrets or unsafe configuration;
- incorrect claims about privacy, anonymity, or on-chain state.

## Safe handling

Never submit real wallet recovery material or private keys as proof. Use Testnet accounts and redact sensitive data. Include the affected repository, commit, contract ID (if applicable), reproduction steps, and impact.

See [docs/SECURITY.md](docs/SECURITY.md) for the suite's documented threat model and trust assumptions.
