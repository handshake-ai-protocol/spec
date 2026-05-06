# handshake-ai-protocol / spec

> **The Handshake Protocol** — an open protocol for cryptographic agent identity, verifiable delegation, and signed action receipts. The audit envelope for the AI agent era.

[![Spec v0.2.3 — Early Access](https://img.shields.io/badge/spec-v0.2.3-06B6D4)](spec/v0.2.3.md)
[![License: CC BY 4.0 (spec) / MIT (code)](https://img.shields.io/badge/license-CC--BY--4.0%20%2F%20MIT-blue)](#license)
[![Working Draft](https://img.shields.io/badge/status-working%20draft-F59E0B)](GOVERNANCE.md)

---

## What this is

The Handshake Protocol defines how AI agents establish verifiable trust with the services they interact with and with each other. Every meaningful agent action begins with a **handshake** — a signed assertion of who's asking, on whose authority, within what limits — and ends with a **receipt** — a signed record of what actually happened. Audit becomes a transcript of handshakes.

This repository contains the **public protocol surface**: the specification text, JSON Schemas (normative), conformance test vectors, and runnable examples. Together these are everything an implementer needs to interoperate with other Handshake-compliant systems.

The protocol is transport-agnostic and designed to compose with the agent communication standards enterprises already use — **MCP**, **A2A**, **OAuth 2.1**, **AP2** — rather than replace them.

## Quickstart

```bash
# Python
pip install handshake-sdk

# TypeScript / Node
npm install @handshake/sdk

# Go
go get github.com/handshake-ai-protocol/handshake-go
```

```python
from handshake import Identity, Agent, Capability

deployer = Identity.generate(kind="org", domain="acme.com")
agent = deployer.spawn_agent(model="claude-sonnet-4-5", instance="job-7f3a")

delegation = deployer.delegate(
    to=agent,
    capabilities=[Capability("billing.invoices.read", max_invoices=100)],
    ttl_seconds=600,
)

async with agent.handshake_with(
    service="https://billing.acme.com/mcp",
    capability="billing.invoices.read",
    delegation=delegation,
) as session:
    invoices = await session.call("invoices.list")
    receipt = session.receipt()
    assert receipt.verify()  # Ed25519 over JCS-canonicalized JSON
```

For the full implementer's guide, see the [public spec](https://handshake.ai/spec) §0 (Quickstart) and §8 (Message formats).

## Repository structure

```
.
├── spec/                       Versioned protocol specifications (Markdown)
│   ├── v0.2.3.md               Current Early Access spec
│   └── README.md               Index of versions
├── schemas/                    Versioned JSON Schemas (normative)
│   └── v0.2.3/
│       ├── _common.json        Shared definitions (DIDs, timestamps, capabilities)
│       ├── delegation-token.json
│       ├── handshake-request.json
│       ├── handshake-acceptance.json
│       ├── handshake-refusal.json
│       ├── receipt.json
│       ├── revocation-statement.json
│       ├── did-document.json
│       └── README.md
├── test-vectors/               Conformance test vectors
│   └── v0.2.3/
│       ├── core/               Required for Core conformance
│       ├── extended/           Required for Extended conformance
│       ├── sovereign/          Required for Sovereign conformance
│       └── README.md
├── examples/                   Runnable example flows (Python, TypeScript)
├── .github/                    Issue templates, PR template, CI
├── README.md                   ← you are here
├── LICENSE-SPEC                CC BY 4.0 (applies to spec text + schemas)
├── LICENSE-CODE                MIT (applies to example code + scripts)
├── CHANGELOG.md                Version history
├── CONTRIBUTING.md             How to propose changes
├── GOVERNANCE.md               Working Group + Foundation framework
├── SECURITY.md                 Vulnerability reporting + PGP key
└── CODE_OF_CONDUCT.md          Standard
```

## Conformance levels

Implementations may claim one of three conformance levels. Each level has a corresponding test-vector suite in `test-vectors/v0.2.3/`. To claim a level, an implementation MUST pass all vectors at that level.

| Level         | What it covers                                                                     | Vectors                              |
|---------------|------------------------------------------------------------------------------------|--------------------------------------|
| **Core**      | Identity, message formats, delegation, receipts, error handling                    | `test-vectors/v0.2.3/core/`          |
| **Extended**  | Core + capability constraint algebra + composition with at least one of (MCP/A2A/OAuth/AP2) | `test-vectors/v0.2.3/extended/`      |
| **Sovereign** | Extended + self-hosted Registry support + BYO-anchor + HSM-backed identity         | `test-vectors/v0.2.3/sovereign/`     |

## Versioning

Handshake follows [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).

- **Patch versions** (`v0.x.Y`) include only clarifications, editorial fixes, and additive constraints that do not affect interoperability.
- **Minor versions** (`v0.X.0`) in the v0.x series MAY include breaking wire-level changes. Each minor version transition publishes a migration guide.
- **Major versions** (`vX.0.0`) at v1.0+ MUST be backwards-compatible at the wire level.
- **Forward compatibility:** receivers MUST tolerate unknown OPTIONAL fields and MUST reject unknown REQUIRED fields with the `protocol_version_unsupported` error code.

Current: **v0.2.3** (Early Access). v1.0 stable freeze targeted 2027 ahead of IETF submission.

## The spec stack

Handshake AI publishes a three-tier spec stack. This repository is **Tier 1**.

- **Tier 1 — Public spec (this repo).** Everything required to interoperate. CC BY 4.0. Free.
- **Tier 2 — Handshake Implementation Guide.** Companion document covering deployment topologies, key management deep dives, performance engineering, Registry implementation, security operations, compliance implementation. NDA-distributed to design partners and Working Group members. Request: [partners@handshake.ai](mailto:partners@handshake.ai).
- **Tier 3 — Internal trade secret.** Specific Registry infrastructure, Console product code, customer-specific integrations. Not distributed.

## Working Group

The Handshake Protocol is governed by the **Handshake Working Group**, a vendor-neutral council convened to evolve the spec across the AI infrastructure ecosystem. See [GOVERNANCE.md](GOVERNANCE.md) for membership criteria, change-proposal process, and Foundation roadmap.

Companies interested in joining the Working Group: [working-group@handshake.ai](mailto:working-group@handshake.ai).

## Contributing

We welcome proposals — typo fixes, clarifying language, new test vectors, errata, and substantive spec changes. Substantive changes follow a structured RFC-style process. See [CONTRIBUTING.md](CONTRIBUTING.md) for the full workflow.

Quick links:
- [Open an issue](https://github.com/handshake-ai-protocol/spec/issues/new/choose)
- [Propose a spec change (RFC)](.github/ISSUE_TEMPLATE/spec-proposal.md)
- [Submit a conformance test vector](test-vectors/v0.2.3/README.md#contributing-vectors)

## Security

Vulnerabilities in the protocol design or in our reference implementations should be reported privately. **Do not open a public issue for a security report.** See [SECURITY.md](SECURITY.md) for our coordinated disclosure policy and PGP key.

## License

- **Specification text and schemas:** [Creative Commons Attribution 4.0 International (CC BY 4.0)](LICENSE-SPEC)
- **Example code, test vectors, scripts:** [MIT License](LICENSE-CODE)

You may implement, derive, redistribute, and commercialize the protocol freely. Attribution to the Handshake Working Group is appreciated for spec derivatives.

## About

The Handshake Protocol is maintained by Handshake AI in partnership with the Handshake Working Group.

- Website: [handshake.ai](https://handshake.ai)
- Spec home: [handshake.ai/spec](https://handshake.ai/spec)
- Working Group inquiries: [working-group@handshake.ai](mailto:working-group@handshake.ai)
- Implementation Guide (NDA): [partners@handshake.ai](mailto:partners@handshake.ai)
- Security: [security@handshake.ai](mailto:security@handshake.ai)

Built by [The Camelback](https://handshake.ai).
