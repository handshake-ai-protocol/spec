# Governance

The Handshake Protocol is intended to be a vendor-neutral open standard. This document describes how the protocol is governed today, who can contribute, how decisions get made, and the path to formal Foundation governance.

## Today (Early Access — 2026)

The protocol is currently maintained by **Handshake AI** as the founding sponsor, with input from a small **Working Group** of design partners and frontier model labs. This is the bootstrap phase.

Decisions are made by:

- **Editorial / clarifying changes** (typo, prose, examples that don't change behavior): a single Handshake AI editor can merge.
- **Schema or wire-level changes** (anything affecting interoperability): require approval from at least two Handshake AI maintainers AND at least one Working Group representative.
- **Security-relevant changes**: require approval from a maintainer designated as security reviewer (currently the founding security cryptographer).
- **Removing or deprecating a feature**: requires a structured RFC-style proposal and a 30-day public comment window before the deprecation can land in a minor version.

## Working Group

The Handshake Working Group is convened to keep the protocol vendor-neutral as it matures. Membership is invited based on the following criteria:

- A meaningful production deployment of, or significant integration with, the protocol
- Engineering capacity to review proposals seriously (not just attend meetings)
- Willingness to operate on the public record (decisions and rationale published)

The current Working Group meets monthly and operates in public for substantive decisions. Meeting notes are published to `meetings/` once approved by attendees.

To request consideration: [working-group@handshake.ai](mailto:working-group@handshake.ai).

## Path to Foundation governance

By **month 18 of the project** (targeted Q4 2027), the protocol stewardship moves to an independent **Handshake Foundation**, modeled on the Cloud Native Computing Foundation (CNCF). Goals of the move:

- Spec changes governed by a multi-stakeholder Technical Steering Committee (TSC), not a single vendor
- Trademark held by the Foundation, licensed back to maintainers including Handshake AI
- Funding from Foundation sponsorships, not from a single commercial entity
- Path to standards-body adoption (IETF RFC) without losing operating velocity

Handshake AI commits to:

- Contributing the spec, schemas, test vectors, and reference implementations to the Foundation under their existing licenses (CC BY 4.0 / MIT)
- Funding the initial Foundation operations
- Participating as one TSC member, with no veto rights

## Change-proposal process (HEPs — Handshake Enhancement Proposals)

Substantive spec changes follow an HEP process:

1. **Draft.** Open a GitHub issue using the [Spec Proposal template](.github/ISSUE_TEMPLATE/spec-proposal.md). Number assigned: HEP-NNNN.
2. **Discussion.** 14-day minimum public discussion. Maintainers and Working Group members weigh in.
3. **Decision.** One of: accept, accept with modifications, defer, or reject. Decisions are recorded in the issue with rationale.
4. **Implementation PR.** If accepted, a PR implementing the change is opened against the next minor version branch.
5. **Final comment period.** 14-day public review of the implementation PR.
6. **Merge.** Lands in the next minor version (`v0.X.0`).

Editorial-only changes skip steps 1–4 and may be merged directly via PR.

## Versioning policy

See [`spec/v0.2.3.md` §15](spec/v0.2.3.md). In short:

- Patch (`v0.x.Y`): editorial / clarifying only
- Minor (`v0.X.0`) in v0.x: MAY be breaking, with migration guide
- Major (`vX.0.0`) at v1.0+: MUST be backwards-compatible at wire level
- Deprecation: features removed no sooner than two minor versions after deprecation announcement

## Conflict resolution

In rare cases of unresolved disagreement among maintainers, the lead maintainer (currently the Handshake AI founding security cryptographer) makes a binding decision and publishes the rationale. Working Group members may file a formal objection that becomes part of the public record.

Once Foundation governance is in place, conflict resolution moves to TSC vote.

## Code of Conduct

All contributors are expected to follow the [Code of Conduct](CODE_OF_CONDUCT.md). Reports go to [conduct@handshake.ai](mailto:conduct@handshake.ai).

## Contact

- General governance questions: [governance@handshake.ai](mailto:governance@handshake.ai)
- Working Group inquiries: [working-group@handshake.ai](mailto:working-group@handshake.ai)
- Standards / IETF coordination: [standards@handshake.ai](mailto:standards@handshake.ai)
