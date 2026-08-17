# Extensions — `pbx_ext`

Not every domain fits in the shared components, and forcing it there would
pollute the standard. `pbx_ext` is the escape hatch: a **typed, versioned**
envelope stored next to `pbx_doc`.

```json
{
  "kind": "<namespace>.<name>",
  "version": "1.0.0",
  "payload": {}
}
```

## Rules

1. `kind` is namespaced and stable; `version` is semver of the payload shape.
2. Consumers **ignore unknown kinds** — never fail on them.
3. `pbx_ext` is never embedded and never rendered on public pages by default;
   it has no capabilities of its own.
4. A payload that turns out to be generic should graduate into a component in a
   future major spec version.
5. Large payloads (>256 KB) live in object storage; `pbx_ext` holds the pointer.

## Registered kinds

| Kind | Version | Used by |
| --- | --- | --- |
| `workflow.definition` | 1.0.0 | `workflow` — graph of nodes/edges plus trigger |
| `task.scheduling` | 1.0.0 | `task` — estimates, dependencies, assignment |
| `plan.breakdown` | 1.0.0 | `plan` — WBS, milestones, critical path |
| `service.definition` | 1.0.0 | `service` — external API manifest: auth, operations, args |
| `design.layout` | 1.0.0 | any — layout plan of blocks bound to JSON Pointers |
| `design.actions` | 1.0.0 | any — declarative JSON-Logic actions on blocks |

### `workflow.definition`

```json
{
  "kind": "workflow.definition",
  "version": "1.0.0",
  "payload": {
    "trigger": {
      "type": "schedule",
      "cron": "0 7 * * *",
      "timezone": "Europe/Amsterdam"
    },
    "nodes": [
      {
        "id": "fetch",
        "type": "service_call",
        "service": "google_mail",
        "operation": "list_messages",
        "args": {
          "query": "is:unread"
        }
      },
      {
        "id": "classify",
        "type": "llm",
        "prompt": "Classify each mail into x, y or z."
      },
      {
        "id": "move",
        "type": "service_call",
        "service": "google_mail",
        "operation": "move_to_label",
        "args": {
          "label": "{{classify.category}}"
        }
      }
    ],
    "edges": [
      {
        "from": "fetch",
        "to": "classify"
      },
      {
        "from": "classify",
        "to": "move"
      }
    ]
  }
}
```

### `task.scheduling`

```json
{
  "kind": "task.scheduling",
  "version": "1.0.0",
  "payload": {
    "estimate_hours": 8,
    "earliest_start": "2026-09-01",
    "dependencies": [
      {
        "task": "pbx:task:1f2e…",
        "type": "finish_to_start",
        "lag_days": 0
      }
    ],
    "assignee": {
      "actor_kind": "ai_agent",
      "ref": "pbx:person_work:agent-01"
    }
  }
}
```
