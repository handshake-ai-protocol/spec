# Security policy

The Handshake Protocol is a security protocol. Vulnerabilities in the protocol design, the reference implementations, or the conformance test vectors can have real, serious consequences for the systems that depend on it.

We take coordinated disclosure seriously and treat security reports with priority and discretion.

## What to report

Please report:

- **Cryptographic weaknesses** in the protocol design (signature schemes used incorrectly, hash collisions, replay vulnerabilities, audience confusion, etc.)
- **Implementation vulnerabilities** in any of the reference SDKs (`handshake-ai-protocol/{python,typescript,go,rust}`)
- **Test vector errors** that allow non-conformant behavior to pass
- **Schema constraints** that fail to reject malformed messages a real implementation should reject
- **Composition risks** with MCP, A2A, OAuth 2.1, or AP2 that the spec does not adequately mitigate
- **Documentation issues** that could lead implementers to insecure deployments

If you're not sure whether something qualifies as security-relevant, err on the side of reporting it through the secure channel below.

## What NOT to report through this channel

The following are bug reports, not security disclosures, and should be filed as normal GitHub issues:

- Typos and editorial issues
- Performance issues without a security impact
- API ergonomic complaints
- Feature requests
- Questions about how to use the protocol

## How to report

Email **security@handshake.ai**. Encrypt with our PGP key (below).

Include:

1. A description of the issue
2. The component affected (spec section, schema file, SDK + version, etc.)
3. A proof-of-concept (minimal example, test vector, or code) if possible
4. The impact you believe it has
5. Whether you've coordinated with anyone else (other vendors, downstream)
6. Your preferred name (or pseudonym) for the eventual public credit

We acknowledge receipt within **2 business days** and provide an initial assessment within **5 business days**.

## Coordinated disclosure timeline

Standard timeline for confirmed vulnerabilities:

| Day | Event |
|---|---|
| 0 | Disclosure received |
| 0–2 | Acknowledgment + initial triage |
| 0–5 | Initial assessment shared with reporter |
| 5–30 | Fix developed, tested, prepared for release |
| 30 | Coordinated release: patch ships, advisory published, reporter credited |
| 30+90 | Detailed write-up published (post-quarantine) |

For critical vulnerabilities being actively exploited, we may shorten the timeline. For complex protocol-level issues requiring multi-vendor coordination, we may extend the timeline up to 90 days. Either way, we communicate with the reporter throughout.

## What you get

- **Acknowledgment** in the [advisories list](https://github.com/handshake-ai-protocol/spec/security/advisories) (unless you prefer anonymity)
- **A bounty** for in-scope, novel vulnerabilities. Bounty program details published at [handshake.ai/security/bounty](https://handshake.ai/security/bounty). Crit/high-severity payouts in the $5,000–$50,000 USD range.
- **Direct communication** with the team during the coordinated disclosure period
- **Co-authorship credit** on the post-quarantine technical write-up if desired

## What we ask of you

- Coordinate with us before public disclosure
- Avoid testing against production systems you don't operate
- Do not exfiltrate data, run denial-of-service attacks, or test in ways that affect real users
- Do not threaten to publish before the coordination period ends

In return, we agree not to pursue legal action against good-faith security research conducted within the bounds of the bounty program.

## PGP key

Fingerprint: `0000 0000 0000 0000 0000 0000 0000 0000 0000 0000`

Key URL: [handshake.ai/.well-known/security.pgp](https://handshake.ai/.well-known/security.pgp)

(The key fingerprint above is a placeholder; the live key is published at the URL.)

## Hall of fame

Researchers who have responsibly disclosed vulnerabilities will be listed here after coordinated public release.

(Empty as of v0.2.3. Be the first.)

## security.txt

A `security.txt` file per [RFC 9116](https://datatracker.ietf.org/doc/html/rfc9116) is published at [handshake.ai/.well-known/security.txt](https://handshake.ai/.well-known/security.txt).
