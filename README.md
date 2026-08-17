# PBX — Product/Project Business eXchange

**Version 2.0.0** · machine-readable standard for describing *any*
business object — an idea, a product, a person, a plan, a task, a workflow — with
one shared document model.

PBX exists because every AI agent, marketplace and CRM re-invents the same
structure. PBX fixes the structure once: a small set of **components**
(PRINCE2-aligned modules such as `metadata`, `productDescription`,
`businessCase`) that are composed into **entities** (45 types today).
Each component is defined by a JSON Schema and carries **capabilities** that tell
tooling how to treat it (searchable, vectorizable, PII, public, translatable).

## Why it works

| Problem | PBX answer |
| --- | --- |
| Every domain needs its own schema | One document, composed of reusable components |
| Agents need to know what is safe to publish | `public_ok` / `pii` capabilities per component |
| Embeddings need structure | `embedAspect` maps components to named vectors |
| Domain-specific payloads | `pbx_ext` — versioned typed extension envelope |

## Read next

- [SPEC.md](SPEC.md) — the document model
- [docs/components.md](docs/components.md) — the 11 components
- [docs/entities.md](docs/entities.md) — the 45 entity types
- [docs/capabilities.md](docs/capabilities.md) — cross-cutting flags
- [docs/state-machines.md](docs/state-machines.md) — lifecycle per format
- [docs/extensions.md](docs/extensions.md) — `pbx_ext` typed payloads
- [docs/integrations.md](docs/integrations.md) — MCP, embed script, WordPress, registry endpoint
- [registry/pbx-registry.json](registry/pbx-registry.json) — machine-readable snapshot
- [schemas/](schemas/) — JSON Schemas per component
- [examples/](examples/) — one example document per core entity

## Reference implementation

[OpenIdeaBox](https://openideabox.com) implements PBX end to end: editor,
semantic search, graph, MCP server and agent tooling. This repository is
generated from that implementation, so the spec and the running code never drift.

## License

The specification, schemas and examples are released under
[CC BY 4.0](LICENSE). Implementations are free to use any license.
