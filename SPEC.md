# PBX Specification v2.0.0

## 1. The document

A PBX record is a JSON object with three parts:

| Field | Type | Purpose |
| --- | --- | --- |
| `format` | string | The entity type (`idea`, `product`, `task`, …) |
| `pbx_doc` | object | The components — the portable, standardised body |
| `pbx_ext` | object \| null | Typed, versioned domain extension (see extensions.md) |

Promoted columns (`title`, `summary`, `status`, `visibility`, `published`)
are derived from `pbx_doc` and exist only for indexing and listing. `pbx_doc`
is always the source of truth.

## 2. Components

`pbx_doc` keys are component ids. Every component is an envelope:

```json
{
  "metadata": {
    "version": "1.0.0",
    "value": {
      "title": "…"
    },
    "provenance": {
      "source": "user",
      "confidence": 0.9
    }
  }
}
```

| Key | Required | Meaning |
| --- | --- | --- |
| `value` | yes | The payload, shaped by the component's JSON Schema |
| `version` | yes | Semver of this module's content; bumped on edit |
| `provenance` | no | Where the value came from (`user`, `ai`, `import`, service id) |
| `confidence` | no | 0–1, mostly written by agents |

Valid component ids: `metadata`, `projectDefinition`, `productDescription`, `businessCase`, `personas`, `scope`, `constraints`, `nonFunctionalRequirements`, `functionalRequirements`, `acceptance`, `references`.

Example of a minimal `pbx_doc`:

```json
{
  "metadata": {
    "version": "1.2.0",
    "updated_at": "2026-08-17T10:00:00Z",
    "value": {
      "title": "Kids party planner",
      "status": "published",
      "tags": [
        "events",
        "family"
      ]
    }
  },
  "productDescription": {
    "version": "1.0.0",
    "value": {
      "tagline": "Plan a birthday party in five minutes",
      "description": "Pick a budget, get a full plan with vendors.",
      "use_cases": [
        "birthday",
        "school event"
      ]
    }
  }
}
```

## 3. Entities

An entity type declares which components it **uses**. Only those components may
appear in `pbx_doc`; anything else is rejected. Each entity also declares which
field feeds the promoted `title` and `summary`.

See [docs/entities.md](docs/entities.md) for the full table.

## 4. Capabilities

Capabilities are declared per component, not per entity, so generic tooling can
act without knowing the domain:

- indexers embed only `vectorizable` components, grouped by `embedAspect`
- public renderers show only `public_ok` components
- GDPR export/delete walks `pii` components
- translation pipelines target `translatable` components

## 5. Addressing

Fields are addressed with **JSON Pointers** relative to the document root:

```text
/metadata/value/title
/productDescription/value/use_cases/0
/businessCase/value/value/revenue_model
```

Layout plans, actions, rules and agent tooling all use these pointers, which
keeps every layer schema-driven instead of template-driven.

## 6. Lifecycle

Formats that model a process declare a state machine: a status field (a JSON
Pointer), an initial state, allowed transitions and allowed actions per state.
Servers enforce transitions; clients only render what is allowed.

See [docs/state-machines.md](docs/state-machines.md).

## 7. Links

Records are connected with typed links (`pbx_links`): `{ from, to, role, weight }`.
Roles are open but conventional: `depends_on`, `part_of`, `related_to`,
`authored_by`, `offers`, `follows`. Weighted links feed graph ranking
(PageRank-style authority) and neighbourhood retrieval for agents.

## 8. Compatibility rules

1. Adding a component to an entity's `uses` is a **minor** change.
2. Removing a component or narrowing a schema is a **major** change.
3. `pbx_ext` payloads carry their own `kind` + `version`; consumers must ignore
   unknown kinds instead of failing.
4. Unknown keys inside `value` are preserved on round-trip, never dropped.
