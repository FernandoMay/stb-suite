# Product overview

## STB Suite

STB Suite explores three different game mechanics on Stellar Soroban. The common product promise is transparent, auditable state transitions rather than simulated runtime interactions.

### 1. ¿SÍ O NEL?

**Tagline:** ¿Tienes razón o nomás tienes confianza?

A social prediction game. Players submit a binary prediction, the prediction becomes immutable on-chain, an authorized resolver publishes the outcome with an evidence hash, and user reputation is derived from contract state.

Core lifecycle:
1. Create prediction.
2. Participate once per wallet before closing.
3. Close under the contract's time and authorization rules.
4. Resolve through an authorized resolver.
5. Read evidence and updated user statistics.

Important distinction: a non-zero evidence hash proves only that a 32-byte value was supplied. It does not, by itself, prove the underlying external evidence is authentic or available.

### 2. TÓMBOLA

**Tagline:** La suerte también se organiza.

A raffle experience with a frozen participant set and an intended verifiable-randomness flow. The product must not select winners using `Math.random`, timestamps, ledger sequence, organizer-selected seeds, transaction hashes, or other predictable/controllable substitutes.

Core lifecycle:
1. Create raffle and define immutable rules.
2. Register participants.
3. Close and freeze entries.
4. Request randomness from the configured provider.
5. Verify fulfillment and derive the winner deterministically.
6. Expose the proof, provider, request, round, and winner for independent reproduction.

The VRF provider's cryptographic and operational trust assumptions must be disclosed. “Uses an oracle” is not equivalent to “trustless.”

### 3. BANDERA ROJA

**Tagline:** Tu opinión es gratis. Tener razón te da puntos.

A social opinion product that distinguishes:
- **Vote/opinion:** expresses a user's preference. Its storage and privacy model must be stated accurately.
- **Prediction:** states which option the user expects to win and is recorded on-chain.
- **Result:** derived from the defined poll rules and authorized publication flow.
- **Score:** awarded only when the result and prediction are resolved, with persistent stats updated and queryable.

Do not describe an off-chain vote as an on-chain prediction or vice versa. Public wallet-linked votes are not anonymous.
