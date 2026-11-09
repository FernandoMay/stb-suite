# QA and release gates

A game may be called **Testnet functional** only when all relevant gates pass.

## Gate A — Source and configuration

- [ ] No demo/mock/fake/simulated runtime path.
- [ ] Search `DEMO_MODE`, `mock`, `fake`, `simulated`, `Math.random`, hardcoded hashes/IDs, `TODO`, `FIXME`.
- [ ] Test-only mocks are isolated and cannot enter production bundle.
- [ ] Network is explicitly Testnet.
- [ ] Contract ID and RPC configuration are validated at startup.
- [ ] Deployment build command, publish directory, redirects, and environment variables are verified against the live site.

## Gate B — Wallet and transactions

- [ ] Correct wallet address and network are shown.
- [ ] Wrong network blocks writes.
- [ ] User authorization is required for each user action.
- [ ] Role authorization is enforced in contract, not only frontend.
- [ ] Signature rejection is handled.
- [ ] Submission, confirmation, failure, and timeout are distinct.
- [ ] Actual transaction hash is captured; empty/missing hash is an error.
- [ ] Explorer link uses the actual confirmed hash.
- [ ] Relevant contract state is read after confirmation.

## Gate C — Product lifecycle

### ¿SÍ O NEL?
- [ ] Create prediction.
- [ ] Participation from at least two wallets.
- [ ] Duplicate participation rejected.
- [ ] Close before deadline rejected.
- [ ] Authorized close after deadline succeeds.
- [ ] Unauthorized close/resolve rejected.
- [ ] Resolver rotation does not strand pending predictions.
- [ ] Resolve with non-zero evidence hash.
- [ ] Read result, evidence reference, and stats for both wallets.

### TÓMBOLA
- [ ] Create raffle and freeze rules.
- [ ] Multiple participants enter.
- [ ] Close freezes participant set.
- [ ] Request randomness from configured provider.
- [ ] Provider/request/raffle binding is verified.
- [ ] Invalid proof rejected.
- [ ] Replayed fulfillment rejected.
- [ ] No predictable fallback exists.
- [ ] Winner can be independently reproduced.
- [ ] Oracle failure leaves raffle pending/failed safely, never invents a winner.

### BANDERA ROJA
- [ ] Vote semantics and storage are explicit.
- [ ] Prediction is a separate action and state.
- [ ] Duplicate vote/prediction rules enforced.
- [ ] Close and result authorization enforced.
- [ ] Tie and minimum-vote rules tested.
- [ ] Result is reproducible.
- [ ] Score is persisted exactly once for every predictor.
- [ ] Multi-wallet `get_user_stats` and ranking match contract state.

## Gate D — Release evidence

- [ ] Fresh `cargo test` result, exact commit, and test count.
- [ ] Fresh frontend test and production build.
- [ ] Deployed contract ID and WASM hash.
- [ ] Confirmed Testnet transaction hashes for critical operations.
- [ ] Post-confirmation state reads.
- [ ] Production URL and deploy commit.
- [ ] Known limitations and unresolved blockers listed.

No aggregate “green” status should hide a failed critical gate.
