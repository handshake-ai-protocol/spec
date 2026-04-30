# JSON Schemas — Handshake Protocol v0.2.3

These schemas are **normative**. The prose in `spec/v0.2.3.md` is informative.

If a message validates against the schema and the prose disagrees with the schema, the schema is correct and the prose has a bug. File an issue.

## Files

| Schema | Description |
|---|---|
| `_common.json` | Shared definitions (DID format, timestamps, hashes, error codes, capabilities) |
| `delegation-token.json` | A signed grant of capability from one principal to another |
| `handshake-request.json` | An agent's request to perform an action against a service |
| `handshake-acceptance.json` | A service's signed acceptance of a HandshakeRequest |
| `handshake-refusal.json` | A service's signed refusal, with typed reason |
| `receipt.json` | A service's signed record of an executed action |
| `revocation-statement.json` | A signed assertion that a delegation or principal is no longer valid |
| `did-document.json` | The Handshake DID Document format (extends W3C DID Core) |

All schemas are JSON Schema 2020-12.

## Using the schemas

### Python (jsonschema)

```python
import json
from jsonschema import Draft202012Validator
from referencing import Registry, Resource

# Load common definitions
common = json.load(open("_common.json"))
schema = json.load(open("handshake-request.json"))

registry = Registry().with_resource(
    "_common.json", Resource.from_contents(common)
)
validator = Draft202012Validator(schema, registry=registry)

# Validate a message
message = json.load(open("my-handshake.json"))
validator.validate(message)
```

### TypeScript / Node (ajv)

```typescript
import Ajv2020 from "ajv/dist/2020";
import common from "./_common.json";
import handshakeRequest from "./handshake-request.json";

const ajv = new Ajv2020();
ajv.addSchema(common, "_common.json");
const validate = ajv.compile(handshakeRequest);

const message = require("./my-handshake.json");
if (!validate(message)) {
  console.error(validate.errors);
}
```

### Go (santhosh-tekuri/jsonschema)

```go
import "github.com/santhosh-tekuri/jsonschema/v6"

c := jsonschema.NewCompiler()
c.AddResource("_common.json", commonReader)
schema, _ := c.Compile("handshake-request.json")
err := schema.Validate(myMessage)
```

## Canonicalization for signing

These schemas validate message **structure**. For signing, messages MUST be canonicalized using JCS (RFC 8785) BEFORE the signature operation. The signature is computed over the JCS-canonicalized form with the `signature` field omitted. See spec §6.3.

A common implementation pitfall is signing the un-canonicalized JSON, which produces signatures that won't verify across implementations. Always canonicalize first.

## Contributing schema changes

Schema changes follow the same RFC-style proposal process as spec changes. See [`../../CONTRIBUTING.md`](../../CONTRIBUTING.md). Schema changes that affect interoperability require a minor version bump (`v0.X.0`).

## License

CC BY 4.0 (same as the spec text).
