# Contributing to the Handshake Protocol

Thanks for the interest. The protocol gets stronger every time someone reads it carefully and finds a thing that's wrong, missing, or unclear.

This document covers four kinds of contribution:

1. [Errata and clarifying changes](#1-errata-and-clarifying-changes)
2. [Conformance test vectors](#2-conformance-test-vectors)
3. [Substantive spec changes (HEPs)](#3-substantive-spec-changes-heps)
4. [Reference implementation contributions](#4-reference-implementation-contributions)

Plus a note on [security disclosures](#security-disclosures), which do **not** go through this process.

---

## 1. Errata and clarifying changes

Examples: typos, broken links, ambiguous prose, inconsistent terminology, wrong cross-references, schema documentation that doesn't match the schema's actual constraints.

**Process:**
1. Open a PR directly. No issue needed for trivial fixes.
2. In the PR description, link to the location in the spec or schema you're fixing.
3. Single-maintainer review and merge. Usually within a week.

These changes land in the next patch version (`v0.x.Y`). They do not affect interoperability.

---

## 2. Conformance test vectors

The conformance test suite is part of the contract. New vectors covering edge cases, attack scenarios, or under-specified behavior are welcome.

**Process:**
1. Add the vector file to the appropriate level directory: `test-vectors/v0.2.3/{core,extended,sovereign}/NNN-short-name.json`.
2. The vector MUST follow the structure documented in [test-vectors/v0.2.3/README.md](test-vectors/v0.2.3/README.md).
3. Open a PR with the new vector. The PR template asks:
   - Which spec section(s) does this vector exercise?
   - Is it positive (must accept) or negative (must reject)?
   - Why isn't this case covered by existing vectors?
   - What threat model or interop concern motivated it?
4. The vector runs against the current reference SDKs in CI. If the vector doesn't pass against the reference SDKs, either the vector or the reference SDKs are wrong — discussed in PR review.
5. Two-maintainer approval, then merge.

Once accepted, vectors become part of the conformance contract. They live forever. Be deliberate.

---

## 3. Substantive spec changes (HEPs — Handshake Enhancement Proposals)

For anything affecting wire-level behavior, conformance, or normative semantics: follow the HEP process.

**Process:**

1. **Open a Spec Proposal issue** using the [Spec Proposal template](.github/ISSUE_TEMPLATE/spec-proposal.md). The issue gets numbered HEP-NNNN. Required content:
   - Motivation (the concrete problem this solves)
   - Detailed design (what the change actually is, with schema diffs and example messages)
   - Alternatives considered
   - Backwards compatibility (does this break existing implementations?)
   - Security and privacy implications
   - Migration plan (if breaking)

2. **Public discussion** for at least 14 days. Maintainers and Working Group members participate.

3. **Decision.** Posted to the issue:
   - **Accepted** — proceed to implementation PR
   - **Accepted with modifications** — proceed with the modifications
   - **Deferred** — good idea, not now (with rationale)
   - **Rejected** — with rationale

4. **Implementation PR** against the next minor version branch (`v0.X.0`). Reference the HEP number.

5. **Final comment period** of 14 days.

6. **Merge** when at least two maintainers and one Working Group representative approve. Security-relevant changes also require security reviewer approval.

7. The change ships in the next minor version (`v0.X.0`) along with a migration guide.

If a proposal has been deferred or rejected, you can re-open with material changes after at least 90 days.

---

## 4. Reference implementation contributions

The reference SDKs live in separate repositories:

- `handshake-ai-protocol/python` (MIT)
- `handshake-ai-protocol/typescript` (MIT)
- `handshake-ai-protocol/go` (MIT)
- `handshake-ai-protocol/rust` (MIT)

Each has its own CONTRIBUTING.md. In general, SDK changes that are wire-protocol-level land here in the spec repo first (via HEP), then propagate to the SDKs.

SDK changes that are purely about ergonomics, performance, or platform-specific concerns can land in the SDK repos directly.

---

## Process expectations

- **Be specific.** "This is wrong" is less useful than "Section 11.2, paragraph 3, claims X but the schema in `delegation-token.json` requires Y. The schema is authoritative — the prose should change."
- **Be explicit about what you're not changing.** PR descriptions should call out what wasn't changed but might appear related.
- **Update tests with code.** PRs that change behavior MUST update or add test vectors.
- **One concept per PR.** A typo fix and a schema change should be two PRs.

## Security disclosures

**Do not file security issues as public GitHub issues or PRs.** See [SECURITY.md](SECURITY.md) for our coordinated disclosure policy and PGP key. Disclosures go to [security@handshake.ai](mailto:security@handshake.ai).

## Licensing of contributions

By contributing, you agree to license your contribution under the same terms as the existing content:

- Spec text and schema changes: CC BY 4.0
- Code contributions (test vectors, scripts): MIT

You retain copyright. You assert that your contribution is original work or that you have the right to contribute it.

A Developer Certificate of Origin (DCO) sign-off is required on commits (`git commit -s`).

## Recognition

Contributors are acknowledged in the [CHANGELOG](CHANGELOG.md) for substantive contributions. Working Group members are credited in the spec.

## Questions

Anything unclear, or a contribution type not covered above: open a discussion or email [governance@handshake.ai](mailto:governance@handshake.ai).
