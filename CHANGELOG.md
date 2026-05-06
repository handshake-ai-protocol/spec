# Changelog

All notable changes to the Handshake Protocol specification, schemas, and conformance test vectors are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) and follows [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added (2026-05-05, ships with the next spec rev — no wire change)

- **§5.1 resolution convention paragraph.** Codifies that `did:hsk:org:<host>` resolves at `https://<host>/.well-known/handshake/did.json` and that the DID Document `id` field MUST string-equal the requested DID (no `alsoKnownAs` chain following). The convention was already implemented by every SDK; this paragraph just makes the contract grep-able.
- **`_common.json#/$defs/did` description update.** Mirrors the §5.1 paragraph so the schema is self-documenting.

### Planned for v0.3 (Q3 2026)

- Hybrid signing (`Hybrid-EdDSA-MLDSA65`) — backwards compatible
- Capability constraint algebra: formal definition of `regex` and `resource_path` intersection
- A2A composition reference normative
- Public key DNS distribution method (informative)
- Migration guide v0.2.3 → v0.3

---

## [0.2.3] — 2026-04-29

### Added

- Audience binding: every signed message MUST now include an `aud` field (§6.7). Receivers MUST reject messages where `aud` does not match.
- Constant-time signature verification SHOULD requirement (§6.6).
- Cryptographic operations table (§7) — explicit mapping of every place crypto happens, what algorithm, what input.
- `protocol_version_unsupported` error code (§14).
- `not_yet_valid` error code for delegations whose `nbf` is in the future (§14).
- Conformance test vectors 005 (aud mismatch), 006 (replay detected), 007 (chain broken).

### Changed

- Cryptographic profile section (§6) reorganized to reference RFCs and FIPS standards explicitly.
- JCS canonicalization elevated from SHOULD to MUST for all signed payloads (§6.3).
- All schemas now reference `_common.json` for shared types instead of duplicating definitions.

### Fixed

- Inconsistency between `result_hash` description in spec (§8.5) and schema (`receipt.json`). Schema was correct; prose updated.
- Multiple typos in §10 (Capabilities) per HEP-0011 errata.

---

## [0.2.2] — 2026-04-12

### Added

- Sub-delegation depth counter (`sub_delegation_depth_remaining`) — bounds maximum chain length (§11).
- Refusal signing requirement (§8.4): refusals MUST be signed.
- Test vectors 003 (scope-exceeded), 004 (invalid-signature).

### Changed

- JCS canonicalization clarified as MUST (was SHOULD).
- `delegable` field semantics for sub-delegation expanded.

---

## [0.2.1] — 2026-03-28

### Changed

- `result_hash` algorithm fixed to SHA-256 (was algorithm-negotiable). SHA-3-256 OPTIONAL alternative declared via `alg` field.

### Fixed

- Schema bug: `delegation_chain` was incorrectly typed as a single object instead of an array.

---

## [0.2.0] — 2026-03-15

### First Early Access release

- Public protocol surface published
- Reference SDKs (Python, TypeScript) ship preview
- Conformance test vectors v0.2.0 (10 core vectors)
- Conformance levels defined: Core, Extended, Sovereign

### Changed from v0.1.x

- `scope.ttl` renamed to `scope.ttl_seconds` for clarity
- `delegation` renamed to `delegation_chain` (now an ordered array)
- Receipt anchoring made OPTIONAL (was REQUIRED in v0.1)
- `aud` field made REQUIRED on DelegationToken (was OPTIONAL)

---

## [0.1.x] — Q1 2026

Closed design-partner releases. Not for public production use.

Changes during this period are documented internally and not enumerated here. Major design decisions from this period:

- Choice of Ed25519 over RSA (smaller signatures, faster verification, modern best practice)
- Choice of JCS over JSON-LD canonicalization (simpler, fewer dependencies)
- Choice of did:hsk method over reusing did:web (need for agent-specific identifier types)
- Decision to keep the protocol transport-agnostic rather than baking in an HTTP profile

---

[Unreleased]: https://github.com/handshake-ai-protocol/spec/compare/v0.2.3...HEAD
[0.2.3]: https://github.com/handshake-ai-protocol/spec/compare/v0.2.2...v0.2.3
[0.2.2]: https://github.com/handshake-ai-protocol/spec/compare/v0.2.1...v0.2.2
[0.2.1]: https://github.com/handshake-ai-protocol/spec/compare/v0.2.0...v0.2.1
[0.2.0]: https://github.com/handshake-ai-protocol/spec/releases/tag/v0.2.0
