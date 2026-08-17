# Integrations

## Registry endpoint

Every PBX implementation should expose a machine-readable snapshot so agents can
discover components and entities at runtime:

```text
GET https://<host>/.well-known/pbx-registry.json
```

The snapshot in [registry/pbx-registry.json](../registry/pbx-registry.json) is the
canonical shape: `{ version, components, entities }`.

## MCP

The reference implementation exposes PBX over the Model Context Protocol so any
agent can create, read, search and link records:

| Tool | Purpose |
| --- | --- |
| `pbx.describe` | Return the registry snapshot |
| `pbx.create` / `pbx.update` | Write a record (schema + state machine enforced) |
| `pbx.get` / `pbx.search` | Read by id or semantic/keyword search |
| `pbx.link` / `pbx.neighbours` | Typed links and graph traversal |
| `pbx.render` | Produce a layout plan for a record |

Two auth modes are supported: an OAuth session, or an API key with an optional
`X-Agent` header so one human account can host several distinctly identified
agents.

## Embed script

A single script tag renders any public PBX record on a third-party page:

```html
<script src="https://<host>/pbx-embed.js" data-pbx-id="<record-id>"></script>
```

Only components with `public_ok` are rendered.

## WordPress / WooCommerce

The `pbx-product-context` plugin maps WooCommerce products onto the `product`
entity, writes PBX JSON plus per-component meta keys, and renders the public
components on the product page. It is a reference for round-trip mapping between
an existing domain model and PBX.

## Agents

Recommended pattern for agent integration:

1. `pbx.describe` once per session for the component/entity contract.
2. Retrieve context with `pbx.search` (aspect-targeted vectors) and
   `pbx.neighbours` (typed links).
3. Write with `pbx.create`/`pbx.update`, always setting `provenance.source = "ai"`
   and a `confidence`.
4. Respect the state machine — read allowed transitions before proposing one.
