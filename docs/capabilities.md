# Capabilities

Capabilities are cross-cutting flags on components. Generic tooling reads them
instead of hard-coding per-format behaviour.

| Capability | Meaning | Components |
| --- | --- | --- |
| `searchable` | Shows up in text search and list previews. | `metadata` `projectDefinition` `productDescription` `businessCase` `personas` `scope` `constraints` `nonFunctionalRequirements` `functionalRequirements` `acceptance` |
| `vectorizable` | Contributes free text to the embedding vectors. | `projectDefinition` `productDescription` `businessCase` `personas` `scope` `functionalRequirements` |
| `pii` | Contains personal data — drives GDPR export/delete and redaction. | `personas` |
| `public_ok` | Safe to render on public or unlisted pages. | `metadata` `productDescription` `businessCase` `references` |
| `mergeable` | Values from multiple sources can be reconciled into one. | — |
| `translatable` | Free text that should be translated when the target language differs. | `productDescription` `personas` |
| `versioned` | The module version is bumped on every edit (default true). | `metadata` `projectDefinition` `productDescription` `businessCase` `personas` `scope` `constraints` `nonFunctionalRequirements` `functionalRequirements` `acceptance` `references` |

## Contracts

- **Indexer** — embeds `vectorizable` components only, grouped per `embedAspect`.
- **Public renderer** — never renders a component without `public_ok`.
- **GDPR** — export and delete walk every `pii` component of every record owned
  by the subject.
- **Merge** — `mergeable` components may be reconciled across sources; others
  are last-writer-wins per module version.
