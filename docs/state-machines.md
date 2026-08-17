# State machines

Formats that model a process declare a lifecycle. Transitions are enforced
server-side on update; clients use the same definition to disable impossible
actions. A format without a state machine has a free-form status.

## `deal`

- **Status field:** `/metadata/value/status`
- **Initial:** `lead`
- **States:** `lead`, `qualified`, `proposal`, `negotiation`, `won`, `lost`, `archived`

```text
lead → qualified
lead → lost
qualified → proposal
qualified → lost
proposal → negotiation
proposal → lost
negotiation → won
negotiation → lost
won → archived
lost → archived
```

**Action restrictions**

| State | Allowed actions |
| --- | --- |
| `won` | `update`, `archive` |
| `lost` | `update`, `archive` |
| `archived` | _none_ |


## `task`

- **Status field:** `/metadata/value/status`
- **Initial:** `todo`
- **States:** `todo`, `in_progress`, `blocked`, `done`, `cancelled`

```text
todo → in_progress
todo → cancelled
in_progress → blocked
in_progress → done
in_progress → cancelled
blocked → in_progress
blocked → cancelled
done → in_progress
```

**Action restrictions**

| State | Allowed actions |
| --- | --- |
| `done` | `update`, `archive` |
| `cancelled` | `update`, `archive` |


## `lead`

- **Status field:** `/metadata/value/status`
- **Initial:** `new`
- **States:** `new`, `contacted`, `qualified`, `converted`, `disqualified`

```text
new → contacted
new → disqualified
contacted → qualified
contacted → disqualified
qualified → converted
qualified → disqualified
```

**Action restrictions**

| State | Allowed actions |
| --- | --- |
| `converted` | `update`, `archive` |
| `disqualified` | `update`, `archive` |


## `invoice`

- **Status field:** `/metadata/value/status`
- **Initial:** `draft`
- **States:** `draft`, `sent`, `paid`, `void`

```text
draft → sent
draft → void
sent → paid
sent → void
```

**Action restrictions**

| State | Allowed actions |
| --- | --- |
| `paid` | `update`, `archive` |
| `void` | `update`, `archive` |


## `subscription`

- **Status field:** `/metadata/value/status`
- **Initial:** `trialing`
- **States:** `trialing`, `active`, `past_due`, `canceled`, `paused`

```text
trialing → active
trialing → canceled
active → past_due
active → paused
active → canceled
past_due → active
past_due → canceled
paused → active
paused → canceled
```

**Action restrictions**

| State | Allowed actions |
| --- | --- |
| `canceled` | `update`, `archive` |


## `message`

- **Status field:** `/metadata/value/status`
- **Initial:** `draft`
- **States:** `draft`, `sent`, `delivered`, `read`, `failed`

```text
draft → sent
sent → delivered
sent → failed
delivered → read
delivered → failed
```

**Action restrictions**

| State | Allowed actions |
| --- | --- |
| `read` | `update`, `archive` |
| `failed` | `update`, `archive` |


## `notification`

- **Status field:** `/metadata/value/status`
- **Initial:** `pending`
- **States:** `pending`, `sent`, `read`, `dismissed`, `failed`

```text
pending → sent
pending → failed
sent → read
sent → dismissed
read → dismissed
```

**Action restrictions**

| State | Allowed actions |
| --- | --- |
| `dismissed` | `update`, `archive` |
| `failed` | `update`, `archive` |


## `email`

- **Status field:** `/metadata/value/status`
- **Initial:** `draft`
- **States:** `draft`, `sent`, `delivered`, `read`, `bounced`, `failed`

```text
draft → sent
sent → delivered
sent → bounced
sent → failed
delivered → read
```

**Action restrictions**

| State | Allowed actions |
| --- | --- |
| `read` | `update`, `archive` |
| `bounced` | `update`, `archive` |
| `failed` | `update`, `archive` |

