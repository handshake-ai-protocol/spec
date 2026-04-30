# Examples

Runnable example flows demonstrating Handshake Protocol usage.

| Example | Language | What it shows |
|---|---|---|
| `python-quickstart/` | Python | The 3-step quickstart from the spec — install, generate identity, first handshake |
| `typescript-quickstart/` | TypeScript / Node | Same flow in TypeScript |
| `mcp-integration/` | Python | Wrapping an existing MCP server with Handshake |
| `multi-step-delegation/` | Python | User → Agent → Sub-agent → Service flow with chain validation |
| `audit-report-export/` | Python | Querying receipts and exporting a SOC2-ready evidence pack |

Each example directory has its own README with setup and run instructions.

These examples are part of the open-source Handshake SDK distribution and live in this repo (rather than a separate `examples` repo) so the spec, schemas, test vectors, and runnable code stay in lockstep version-by-version.

## Status

- Examples for v0.2.3 land alongside the SDK preview release in the next sprint
- Until then, see the [SDK quickstart](https://docs.handshake.ai/quickstart) and the spec's §0 (Implementer's Quickstart)

## License

MIT, same as all code in this repo. See [`../LICENSE-CODE`](../LICENSE-CODE).
