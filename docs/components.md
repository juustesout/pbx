# Components

A component is one PRINCE2-aligned module of a PBX document. Component ids are
stable — they are the top-level keys of `pbx_doc`.

| id | Label | JSON Schema | Capabilities | Embed aspect |
| --- | --- | --- | --- | --- |
| `metadata` | Metadata | [metadata_expanded.json](../schemas/metadata_expanded.json) | `searchable` `public_ok` `versioned` | `intent` |
| `projectDefinition` | Project definition | [project-definition_expanded.json](../schemas/project-definition_expanded.json) | `searchable` `vectorizable` `versioned` | `intent` |
| `productDescription` | Product description | [product-description_expanded.json](../schemas/product-description_expanded.json) | `searchable` `vectorizable` `public_ok` `translatable` `versioned` | `functional` |
| `businessCase` | Business case | [business-case_expanded.json](../schemas/business-case_expanded.json) | `searchable` `vectorizable` `public_ok` `versioned` | `quality` |
| `personas` | Personas | [personas_expanded.json](../schemas/personas_expanded.json) | `searchable` `vectorizable` `pii` `translatable` `versioned` | `personal` |
| `scope` | Scope | [scope_expanded.json](../schemas/scope_expanded.json) | `searchable` `vectorizable` `versioned` | `functional` |
| `constraints` | Constraints | [constraints_expanded.json](../schemas/constraints_expanded.json) | `searchable` `versioned` | `quality` |
| `nonFunctionalRequirements` | Non-functional requirements | [non-functional-requirements_expanded.json](../schemas/non-functional-requirements_expanded.json) | `searchable` `versioned` | `quality` |
| `functionalRequirements` | Functional requirements | [functional-requirements_expanded.json](../schemas/functional-requirements_expanded.json) | `searchable` `vectorizable` `versioned` | `functional` |
| `acceptance` | Acceptance | [acceptance_expanded.json](../schemas/acceptance_expanded.json) | `searchable` `versioned` | `quality` |
| `references` | References | [references_expanded.json](../schemas/references_expanded.json) | `public_ok` `versioned` | — |

## Embed aspects

- `intent` — What the thing is and why it exists.
- `functional` — What it does — features, use cases, scope.
- `quality` — How good/viable it is — business case, constraints, acceptance.
- `personal` — Who it is about — personas, people.

Aspects map onto named vectors in the vector store, so a query can target
"functional match" separately from "who is this about".
