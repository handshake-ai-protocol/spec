# Specification — versioned

The Handshake Protocol specification, by version. The newest stable version of any minor series is the canonical one for that series.

| Version | Status | Released | Notes |
|---|---|---|---|
| [v0.2.3](v0.2.3.md) | **Early Access (current)** | 2026-04-29 | Adds audience binding, JCS MUST, crypto operations table |
| v0.2.2 | Superseded | 2026-04-12 | Sub-delegation depth, refusal signing |
| v0.2.1 | Superseded | 2026-03-28 | result_hash algorithm fix |
| v0.2.0 | Superseded | 2026-03-15 | First Early Access release |
| v0.1.x | Closed (design partner only) | Q1 2026 | Not for public production use |

The full historical change log lives in [CHANGELOG.md](../CHANGELOG.md) at the repo root.

The HTML / web-rendered version of the current spec lives at [handshake.ai/spec](https://handshake.ai/spec).

## Conformance

Implementations conformant with a given version MUST pass the corresponding test vectors at the conformance level they claim. See [`../test-vectors/`](../test-vectors/) and the spec's §16.

## Versioning policy

See spec §15 (Versioning policy). In short:

- Patch releases (`v0.x.Y`) are editorial only
- Minor releases (`v0.X.0`) in the v0.x series MAY be breaking, with a migration guide
- Major releases (`vX.0.0`) at v1.0+ MUST be backwards-compatible at wire level
- Two-minor-version overlap before any deprecation is removed
