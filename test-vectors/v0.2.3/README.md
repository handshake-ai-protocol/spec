# Conformance Test Vectors — Handshake Protocol v0.2.3

These vectors define what "Handshake-compliant" means at this protocol version. Implementations claiming a conformance level (Core, Extended, Sovereign — see spec §16) MUST pass all vectors at that level.

## Structure

Each test vector is a JSON file with the following top-level fields:

```jsonc
{
  "vector_id": "001-valid-handshake",
  "spec_version": "0.2.3",
  "category": "core",                     // core | extended | sovereign
  "description": "...",                   // human-readable summary
  "spec_references": ["§5.1", "§9.1"],   // sections of the spec this exercises
  "input": { /* the message(s) to verify */ },
  "context": { /* keys, time, registry state needed for verification */ },
  "expected": { /* expected verification outcome */ },
  "notes": "..."                          // implementer guidance, optional
}
```

The `expected` block specifies what a conformant implementation MUST produce. For positive vectors (`expected.result: "accept"`), the verifier MUST accept. For negative vectors (`expected.result: "reject"`), the verifier MUST reject AND MUST identify the cause (`expected.error_code`).

## Running the vectors

A reference vector runner is published with each SDK:

```bash
# Python
python -m handshake.conformance --level=core --vectors-dir=./core/

# TypeScript
npx handshake-conformance --level=core --vectors-dir=./core/

# Go
handshake-conform -level core -vectors ./core/
```

## Categories

```
core/         Required for Core conformance — identity, message formats,
              signature verification, delegation chain walk, basic receipts,
              error handling.
extended/     Required for Extended conformance — capability constraint
              algebra, composition with at least one of MCP/A2A/OAuth/AP2.
sovereign/    Required for Sovereign conformance — self-hosted Registry,
              BYO-anchor, HSM-backed identity attestation.
```

## Time and randomness

Vectors that depend on the current time include a `context.now` field — verifiers MUST use this fixed time during conformance testing rather than the system clock. Vectors that depend on randomness include all required random material in the `context` block.

## Cryptographic material

Test vectors include real Ed25519 keypairs and signatures. **These keys are for testing only.** Do NOT use any test-vector key in production.

Each vector that involves signature verification includes:
- `context.public_keys`: a map of DID → Ed25519 public key (base64url)
- `context.private_keys`: a map of DID → Ed25519 private key (base64url) — only present in vectors that require generating new signatures

## Contributing vectors

We welcome new test vectors covering edge cases, attack scenarios, and underspecified behavior. Open a PR adding the vector file. The PR template asks for:

1. Which spec section(s) the vector exercises
2. Whether the vector is positive (must accept) or negative (must reject)
3. Why this case isn't covered by existing vectors
4. Optionally, a brief writeup of the threat or interop concern motivating it

Vectors live forever once accepted — they become part of the conformance contract. Be deliberate.

## Vector index

### Core

| ID | Description | Positive/Negative |
|---|---|---|
| `001-valid-handshake` | Single-link delegation, valid signatures, in-scope capability | Positive |
| `002-expired-delegation` | Delegation past `exp`, otherwise valid | Negative — `expired` |
| `003-scope-exceeded` | Requested constraints exceed delegation grant | Negative — `scope_exceeded` |
| `004-invalid-signature` | Tampered signature byte | Negative — `signature_invalid` |
| `005-aud-mismatch` | Request `aud` doesn't match service DID | Negative — `aud_mismatch` |
| `006-replay-detected` | Repeat nonce within TTL window | Negative — `replay_detected` |
| `007-chain-broken` | Middle delegation `aud` doesn't match next `iss` | Negative — `chain_broken` |
| `008-credential-revoked` | Delegation issuer published a revocation | Negative — `credential_revoked` |
| `009-receipt-roundtrip` | Sign + verify a receipt against expected hash | Positive |
| `010-jcs-canonicalization` | Same logical message, different key ordering — must verify | Positive |

(Additional vectors in this directory.)

### Extended

(See `extended/` for capability constraint algebra and composition vectors.)

### Sovereign

(See `sovereign/` for Registry, BYO-anchor, HSM-backed identity vectors.)

## License

CC BY 4.0 (vectors and prose) / MIT (any vector-runner scripts).
