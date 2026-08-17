# Entity types

45 entity types are defined. Each one composes components
and declares the editor fields that map onto JSON Pointers.

| Type | Label | What it is | Uses |
| --- | --- | --- | --- |
| 💡 `idea` | Idea | A raw idea — problem, solution sketch, who it's for. | `metadata` `productDescription` `scope` `personas` `businessCase` |
| 🗺️ `plan` | Plan | A parent container that turns an idea into work — tasks & runs hang off it. | `metadata` `projectDefinition` `businessCase` `scope` `acceptance` |
| 📁 `project` | Project | A container above Plan — long-lived initiative with multiple plans/tasks. | `metadata` `projectDefinition` `scope` `acceptance` |
| ✅ `task` | Task | A macro-task in a plan. Micro-steps live inline in pbx_ext.data.steps[] and are not first-class records. | `metadata` `projectDefinition` `scope` `acceptance` `constraints` |
| 🔗 `workflow` | Workflow | A generic executable workflow (n8n, LangGraph, Temporal, …). Provider lives in pbx_ext.data.provider; large definitions go to object storage as definition_ref. | `metadata` `productDescription` `businessCase` `constraints` |
| 🌱 `lead` | Lead | An unqualified prospect — top of the sales pipeline. | `metadata` `productDescription` `personas` `businessCase` |
| 🤝 `deal` | Deal | An in-flight sales opportunity moving through a pipeline. | `metadata` `productDescription` `businessCase` `acceptance` |
| 🎯 `opportunity` | Opportunity | A larger, multi-stage revenue chance — often a family of deals. | `metadata` `productDescription` `businessCase` `scope` |
| 📦 `product` | Product | A sellable thing — physical or digital. | `metadata` `productDescription` `businessCase` `constraints` |
| 🛠️ `service` | Service | A sellable non-physical offering — sibling of Product. | `metadata` `productDescription` `businessCase` `constraints` |
| 🏢 `company` | Company | An org — what you do, who you serve, how to reach you. | `metadata` `productDescription` |
| 🏬 `vendor` | Vendor | A supplier or service provider you buy from. | `metadata` `productDescription` `businessCase` |
| 📇 `contact` | Contact | A person outside your team — someone you talk to but who has no login. | `metadata` `productDescription` `personas` |
| ❤️ `person_dating` | You — dating | How you show up to a potential partner. | `metadata` `productDescription` `personas` `constraints` |
| 👥 `person_social` | You — social | You among friends and communities. | `metadata` `productDescription` `personas` |
| 💼 `person_work` | Actor — work | A working actor — human, AI agent, service account, or robot. Role, skills, availability. | `metadata` `productDescription` `personas` `businessCase` `constraints` |
| 📢 `job_opening` | Job opening | A role you're hiring for. | `metadata` `productDescription` `businessCase` `nonFunctionalRequirements` |
| 📜 `knowledge_asset` | Knowledge asset | Executable knowledge — a template, contract, or checklist you can buy and use. | `metadata` `productDescription` `businessCase` `constraints` `personas` |
| ⚡ `micro_app` | Micro-app | A small executable tool, AI helper, or challenge object. | `metadata` `productDescription` `businessCase` `personas` `constraints` |
| 🎯 `challenge` | Challenge | A short quiz with a personalized score and a shareable link. | `metadata` `productDescription` `personas` `constraints` |
| 📅 `event` | Event | A calendar event with a start and end. | `metadata` `productDescription` |
| 👥 `meeting` | Meeting | An event subtype with attendees and an agenda. | `metadata` `productDescription` `acceptance` |
| 📞 `call` | Call | A logged phone or video interaction. | `metadata` `productDescription` |
| 📊 `activity` | Activity | A generic timeline entry — anything worth remembering happened. | `metadata` `productDescription` |
| 📄 `doc` | Doc | A knowledge document with a markdown body. | `metadata` `productDescription` `references` |
| 🗒️ `note` | Note | A short user note. | `metadata` `productDescription` |
| 📎 `file` | File | A wrapper around a stored object — points at a storage bucket path. | `metadata` `productDescription` |
| 🏷️ `tag` | Tag | A canonical tag from your taxonomy. | `metadata` `productDescription` |
| 🏷️ `price` | Price | A catalog price: currency, amount, interval, and validity window. | `metadata` `productDescription` `businessCase` |
| 📦 `billing_plan` | Billing Plan | A pricing plan grouping one or more prices + entitlements. | `metadata` `productDescription` `businessCase` `functionalRequirements` |
| 🧾 `invoice` | Invoice | A billable invoice with lines, totals, and Draft→Sent→Paid state. | `metadata` `productDescription` `businessCase` `references` |
| 💳 `payment` | Payment | A settled or attempted payment against an invoice or SKU. | `metadata` `productDescription` `references` |
| 🔁 `subscription` | Subscription | A recurring plan against a price, with lifecycle state. | `metadata` `productDescription` `businessCase` |
| 🔑 `license` | License | A capability grant to an actor for a bundle, with optional expiry. | `metadata` `productDescription` `constraints` |
| 👛 `wallet` | Wallet | A credit balance for an actor. Ledger-backed elsewhere. | `metadata` `productDescription` |
| 💬 `conversation` | Conversation | A 1:1 or group conversation grouping threads and messages. | `metadata` `productDescription` `personas` |
| 🧵 `thread` | Thread | A single topical thread inside a conversation or channel. | `metadata` `productDescription` |
| 📣 `channel` | Channel | A named channel for broadcasting or group discussion. | `metadata` `productDescription` |
| ✉️ `message` | Message | A single message inside a conversation, thread, or channel. | `metadata` `productDescription` |
| 📧 `email` | Email | An outbound or inbound email with subject and body. | `metadata` `productDescription` |
| 🔔 `notification` | Notification | A short alert for one recipient, delivered in-app or via a channel. | `metadata` `productDescription` |
| 📡 `broadcast` | Broadcast | A one-to-many announcement fanned out to a channel or list. | `metadata` `productDescription` `personas` |
| 📥 `inbox` | Inbox | An owner's collection of incoming messages/notifications. | `metadata` `productDescription` |
| 📤 `outbox` | Outbox | An owner's queue of outgoing messages/broadcasts. | `metadata` `productDescription` |
| 🪝 `webhook` | Webhook | An outbound webhook endpoint receiving events for a record or channel. | `metadata` `productDescription` |

---

### 💡 Idea — `idea`

A raw idea — problem, solution sketch, who it's for.

- **Uses:** `metadata`, `productDescription`, `scope`, `personas`, `businessCase`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`


**Pitch**

| Field | Pointer | Kind |
| --- | --- | --- |
| Title | `/metadata/value/title` | text |
| Tagline | `/productDescription/value/tagline` | text |
| The idea | `/productDescription/value/description` | markdown |

**Problem & audience**

| Field | Pointer | Kind |
| --- | --- | --- |
| Problem it solves | `/scope/value/problem` | textarea |
| Who it's for | `/personas/value/target_audience` | textarea |
| Example use cases | `/productDescription/value/use_cases` | chips |

**Business**

| Field | Pointer | Kind |
| --- | --- | --- |
| Willingness to pay (EUR) | `/businessCase/value/value/willingness_to_pay` | text |
| Revenue model | `/businessCase/value/value/revenue_model` | text |
| Competitors | `/businessCase/value/value/competitors` | chips |


---

### 🗺️ Plan — `plan`

A parent container that turns an idea into work — tasks & runs hang off it.

- **Uses:** `metadata`, `projectDefinition`, `businessCase`, `scope`, `acceptance`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/projectDefinition/value/objective`


**Basics**

| Field | Pointer | Kind |
| --- | --- | --- |
| Plan title | `/metadata/value/title` | text |
| Objective | `/projectDefinition/value/objective` | textarea |
| Background / context | `/projectDefinition/value/background` | markdown |

**Scope & outcome**

| Field | Pointer | Kind |
| --- | --- | --- |
| In scope | `/scope/value/in_scope` | chips |
| Out of scope | `/scope/value/out_of_scope` | chips |
| Acceptance criteria | `/acceptance/value/criteria` | chips |

**Business case**

| Field | Pointer | Kind |
| --- | --- | --- |
| Value / revenue model | `/businessCase/value/value/revenue_model` | text |
| Willingness to pay | `/businessCase/value/value/willingness_to_pay` | text |


---

### 📁 Project — `project`

A container above Plan — long-lived initiative with multiple plans/tasks.

- **Uses:** `metadata`, `projectDefinition`, `scope`, `acceptance`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/projectDefinition/value/objective`


**Project**

| Field | Pointer | Kind |
| --- | --- | --- |
| Project name | `/metadata/value/title` | text |
| Objective | `/projectDefinition/value/objective` | textarea |
| Status | `/metadata/value/status` | select |

**Scope**

| Field | Pointer | Kind |
| --- | --- | --- |
| In scope | `/scope/value/in_scope` | chips |
| Out of scope | `/scope/value/out_of_scope` | chips |
| Acceptance criteria | `/acceptance/value/criteria` | chips |


---

### ✅ Task — `task`

A macro-task in a plan. Micro-steps live inline in pbx_ext.data.steps[] and are not first-class records.

- **Uses:** `metadata`, `projectDefinition`, `scope`, `acceptance`, `constraints`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/projectDefinition/value/objective`
- **Lifecycle:** `todo` → `in_progress` → `blocked` → `done` → `cancelled`

**Basics**

| Field | Pointer | Kind |
| --- | --- | --- |
| Task title | `/metadata/value/title` | text |
| What done looks like | `/projectDefinition/value/objective` | textarea |
| Status | `/metadata/value/status` | select |

**Planning**

| Field | Pointer | Kind |
| --- | --- | --- |
| Assignee (person_work id or handle) | `/metadata/value/assignee` | text |
| Due date (ISO) | `/metadata/value/due` | text |
| Estimated duration | `/metadata/value/duration` | text |

**Acceptance & scope**

| Field | Pointer | Kind |
| --- | --- | --- |
| Acceptance criteria | `/acceptance/value/criteria` | chips |
| In scope | `/scope/value/in_scope` | chips |
| Known blockers | `/constraints/value/blockers` | chips |


---

### 🔗 Workflow — `workflow`

A generic executable workflow (n8n, LangGraph, Temporal, …). Provider lives in pbx_ext.data.provider; large definitions go to object storage as definition_ref.

- **Uses:** `metadata`, `productDescription`, `businessCase`, `constraints`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/summary`


**Basics**

| Field | Pointer | Kind |
| --- | --- | --- |
| Workflow title | `/metadata/value/title` | text |
| What this workflow does | `/productDescription/value/summary` | textarea |
| Status | `/metadata/value/status` | select |

**Provider & handle**

| Field | Pointer | Kind |
| --- | --- | --- |
| Provider | `/metadata/value/provider` | select |
| External workflow id / handle | `/metadata/value/external_id` | text |
| Instance URL | `/metadata/value/instance_url` | url |
| Trigger webhook URL (optional) | `/metadata/value/webhook_url` | url |

**Business & constraints**

| Field | Pointer | Kind |
| --- | --- | --- |
| Value / purpose | `/businessCase/value/value/revenue_model` | text |
| Required credentials (handles only) | `/constraints/value/credentials` | chips |
| Rate limits / cadence | `/constraints/value/rate_limits` | text |


---

### 🌱 Lead — `lead`

An unqualified prospect — top of the sales pipeline.

- **Uses:** `metadata`, `productDescription`, `personas`, `businessCase`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`
- **Lifecycle:** `new` → `contacted` → `qualified` → `converted` → `disqualified`

**Lead**

| Field | Pointer | Kind |
| --- | --- | --- |
| Name / company | `/metadata/value/title` | text |
| Source | `/metadata/value/source` | text |
| Status | `/metadata/value/status` | select |
| Interest | `/productDescription/value/tagline` | text |

**Value**

| Field | Pointer | Kind |
| --- | --- | --- |
| Est. deal size | `/businessCase/value/value/willingness_to_pay` | text |
| Audience / fit | `/personas/value/target_audience` | textarea |


---

### 🤝 Deal — `deal`

An in-flight sales opportunity moving through a pipeline.

- **Uses:** `metadata`, `productDescription`, `businessCase`, `acceptance`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`
- **Lifecycle:** `lead` → `qualified` → `proposal` → `negotiation` → `won` → `lost` → `archived`

**Deal**

| Field | Pointer | Kind |
| --- | --- | --- |
| Deal name | `/metadata/value/title` | text |
| Stage | `/metadata/value/status` | select |
| Expected close date | `/metadata/value/close_date` | text |

**Value**

| Field | Pointer | Kind |
| --- | --- | --- |
| Amount | `/businessCase/value/value/amount` | text |
| Currency | `/businessCase/value/value/currency` | text |
| Probability (%) | `/businessCase/value/value/probability` | number |

**Acceptance**

| Field | Pointer | Kind |
| --- | --- | --- |
| What closes this deal | `/acceptance/value/criteria` | chips |


---

### 🎯 Opportunity — `opportunity`

A larger, multi-stage revenue chance — often a family of deals.

- **Uses:** `metadata`, `productDescription`, `businessCase`, `scope`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`


**Opportunity**

| Field | Pointer | Kind |
| --- | --- | --- |
| Opportunity name | `/metadata/value/title` | text |
| Description | `/productDescription/value/description` | markdown |
| Stage | `/metadata/value/status` | select |

**Scope & value**

| Field | Pointer | Kind |
| --- | --- | --- |
| In scope | `/scope/value/in_scope` | chips |
| Est. value | `/businessCase/value/value/amount` | text |
| Currency | `/businessCase/value/value/currency` | text |


---

### 📦 Product — `product`

A sellable thing — physical or digital.

- **Uses:** `metadata`, `productDescription`, `businessCase`, `constraints`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`


**Basics**

| Field | Pointer | Kind |
| --- | --- | --- |
| Product name | `/metadata/value/title` | text |
| Short pitch | `/productDescription/value/tagline` | text |
| Description | `/productDescription/value/description` | markdown |

**Commerce**

| Field | Pointer | Kind |
| --- | --- | --- |
| Regular price | `/businessCase/value/pricing/regularPrice` | text |
| Sale price | `/businessCase/value/pricing/salePrice` | text |
| Currency | `/businessCase/value/pricing/currency` | text |
| SKU | `/constraints/value/inventory/sku` | text |
| Stock status | `/constraints/value/inventory/stockStatus` | select |

**Story & fit**

| Field | Pointer | Kind |
| --- | --- | --- |
| Ideal buyer | `/productDescription/value/target_audience` | textarea |
| Key features | `/productDescription/value/key_features` | chips |
| Use cases | `/productDescription/value/use_cases` | chips |


---

### 🛠️ Service — `service`

A sellable non-physical offering — sibling of Product.

- **Uses:** `metadata`, `productDescription`, `businessCase`, `constraints`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`


**Service**

| Field | Pointer | Kind |
| --- | --- | --- |
| Service name | `/metadata/value/title` | text |
| Short pitch | `/productDescription/value/tagline` | text |
| Description | `/productDescription/value/description` | markdown |

**Pricing**

| Field | Pointer | Kind |
| --- | --- | --- |
| Price | `/businessCase/value/pricing/regularPrice` | text |
| Currency | `/businessCase/value/pricing/currency` | text |
| Unit | `/businessCase/value/pricing/unit` | text |

**Constraints**

| Field | Pointer | Kind |
| --- | --- | --- |
| Availability | `/constraints/value/availability` | text |


---

### 🏢 Company — `company`

An org — what you do, who you serve, how to reach you.

- **Uses:** `metadata`, `productDescription`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`


**Identity**

| Field | Pointer | Kind |
| --- | --- | --- |
| Company name | `/metadata/value/title` | text |
| One-line pitch | `/productDescription/value/tagline` | text |
| About | `/productDescription/value/description` | markdown |
| Website | `/metadata/value/website` | url |

**Profile**

| Field | Pointer | Kind |
| --- | --- | --- |
| Sector / industry | `/metadata/value/sector` | text |
| Team size | `/metadata/value/size` | select |
| Founded (year) | `/metadata/value/founded` | text |
| We serve | `/productDescription/value/target_audience` | textarea |
| Services / offerings | `/productDescription/value/services` | chips |


---

### 🏬 Vendor — `vendor`

A supplier or service provider you buy from.

- **Uses:** `metadata`, `productDescription`, `businessCase`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`


**Vendor**

| Field | Pointer | Kind |
| --- | --- | --- |
| Vendor name | `/metadata/value/title` | text |
| What they offer | `/productDescription/value/tagline` | text |
| Categories | `/productDescription/value/services` | chips |
| Website | `/metadata/value/website` | url |

**Terms**

| Field | Pointer | Kind |
| --- | --- | --- |
| Rate / typical price | `/businessCase/value/rate` | text |
| Payment terms | `/businessCase/value/payment_terms` | text |


---

### 📇 Contact — `contact`

A person outside your team — someone you talk to but who has no login.

- **Uses:** `metadata`, `productDescription`, `personas`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`


**Identity**

| Field | Pointer | Kind |
| --- | --- | --- |
| Full name | `/metadata/value/title` | text |
| Company | `/metadata/value/company` | text |
| Role / title | `/personas/value/role` | text |
| Short note | `/productDescription/value/tagline` | text |

**Reach**

| Field | Pointer | Kind |
| --- | --- | --- |
| Email | `/metadata/value/email` | text |
| Phone (E.164) | `/metadata/value/phone` | text |
| Website | `/metadata/value/website` | url |


---

### ❤️ You — dating — `person_dating`

How you show up to a potential partner.

- **Uses:** `metadata`, `productDescription`, `personas`, `constraints`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`


**Basics**

| Field | Pointer | Kind |
| --- | --- | --- |
| Display name | `/metadata/value/title` | text |
| Avatar URL | `/metadata/value/avatar_url` | url |
| Tagline | `/productDescription/value/tagline` | text |
| About you | `/productDescription/value/summary` | markdown |

**Details**

| Field | Pointer | Kind |
| --- | --- | --- |
| Age | `/personas/value/age` | number |
| Height (cm) | `/personas/value/height_cm` | number |
| Eye color | `/personas/value/eye_color` | text |
| Looking for | `/personas/value/relationship_goal` | select |

**Wants & deal-breakers**

| Field | Pointer | Kind |
| --- | --- | --- |
| What you're looking for | `/personas/value/looking_for` | textarea |
| Deal-breakers | `/constraints/value/dealbreakers` | textarea |
| Interests | `/personas/value/interests` | chips |
| Languages | `/personas/value/languages` | chips |


---

### 👥 You — social — `person_social`

You among friends and communities.

- **Uses:** `metadata`, `productDescription`, `personas`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`


**Basics**

| Field | Pointer | Kind |
| --- | --- | --- |
| Display name | `/metadata/value/title` | text |
| Avatar URL | `/metadata/value/avatar_url` | url |
| Tagline | `/productDescription/value/tagline` | text |
| About you | `/productDescription/value/summary` | markdown |

**Circles**

| Field | Pointer | Kind |
| --- | --- | --- |
| Interests | `/personas/value/interests` | chips |
| Communities | `/personas/value/communities` | chips |
| Languages | `/personas/value/languages` | chips |


---

### 💼 Actor — work — `person_work`

A working actor — human, AI agent, service account, or robot. Role, skills, availability.

- **Uses:** `metadata`, `productDescription`, `personas`, `businessCase`, `constraints`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`


**Basics**

| Field | Pointer | Kind |
| --- | --- | --- |
| Display name | `/metadata/value/title` | text |
| Actor kind | `/metadata/value/kind` | select |
| Avatar URL | `/metadata/value/avatar_url` | url |
| Role / title | `/personas/value/role` | text |
| One-line pitch | `/productDescription/value/tagline` | text |
| About your work | `/productDescription/value/summary` | markdown |

**Skills & experience**

| Field | Pointer | Kind |
| --- | --- | --- |
| Skills | `/personas/value/skills` | chips |
| Years of experience | `/personas/value/years_experience` | number |
| Languages | `/personas/value/languages` | chips |

**Availability**

| Field | Pointer | Kind |
| --- | --- | --- |
| Rate | `/businessCase/value/rate` | text |
| Availability | `/businessCase/value/availability` | text |
| Preferences / constraints | `/constraints/value/prefs` | textarea |

**Non-human handles**

| Field | Pointer | Kind |
| --- | --- | --- |
| Provider (ai_agent / service / robot) | `/metadata/value/provider` | text |
| External id / handle | `/metadata/value/external_id` | text |
| Endpoint / webhook URL | `/metadata/value/endpoint_url` | url |


---

### 📢 Job opening — `job_opening`

A role you're hiring for.

- **Uses:** `metadata`, `productDescription`, `businessCase`, `nonFunctionalRequirements`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`


**Role**

| Field | Pointer | Kind |
| --- | --- | --- |
| Job title | `/metadata/value/title` | text |
| Company | `/metadata/value/company` | text |
| One-line pitch | `/productDescription/value/tagline` | text |
| Job description | `/productDescription/value/description` | markdown |

**Requirements**

| Field | Pointer | Kind |
| --- | --- | --- |
| Must have | `/productDescription/value/must_have` | chips |
| Nice to have | `/productDescription/value/nice_to_have` | chips |
| Skills | `/productDescription/value/skills` | chips |
| Seniority | `/productDescription/value/seniority` | select |

**Comp & logistics**

| Field | Pointer | Kind |
| --- | --- | --- |
| Compensation | `/businessCase/value/salary` | text |
| Employment type | `/businessCase/value/employment_type` | select |
| Location | `/nonFunctionalRequirements/value/location` | text |
| Remote policy | `/nonFunctionalRequirements/value/remote` | select |


---

### 📜 Knowledge asset — `knowledge_asset`

Executable knowledge — a template, contract, or checklist you can buy and use.

- **Uses:** `metadata`, `productDescription`, `businessCase`, `constraints`, `personas`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`


**Basics**

| Field | Pointer | Kind |
| --- | --- | --- |
| Title | `/metadata/value/title` | text |
| One-line pitch | `/productDescription/value/tagline` | text |
| Preview (public markdown) | `/productDescription/value/description` | markdown |

**Applicability**

| Field | Pointer | Kind |
| --- | --- | --- |
| Jurisdiction | `/personas/value/jurisdiction` | chips |
| Company size | `/personas/value/company_size` | chips |
| Languages | `/personas/value/languages` | chips |

**Commerce**

| Field | Pointer | Kind |
| --- | --- | --- |
| SKU | `/businessCase/value/pricing/sku` | text |
| Price | `/businessCase/value/pricing/regularPrice` | text |
| Currency | `/businessCase/value/pricing/currency` | text |

**Gated content**

| Field | Pointer | Kind |
| --- | --- | --- |
| Full document (markdown, unlock-gated) | `/constraints/value/contract_template` | markdown |


---

### ⚡ Micro-app — `micro_app`

A small executable tool, AI helper, or challenge object.

- **Uses:** `metadata`, `productDescription`, `businessCase`, `personas`, `constraints`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`


**Basics**

| Field | Pointer | Kind |
| --- | --- | --- |
| App name | `/metadata/value/title` | text |
| One-line pitch | `/productDescription/value/tagline` | text |
| What it does | `/productDescription/value/description` | markdown |

**Audience**

| Field | Pointer | Kind |
| --- | --- | --- |
| Who it's for | `/personas/value/target_audience` | textarea |
| Example use cases | `/productDescription/value/use_cases` | chips |
| Languages | `/personas/value/languages` | chips |

**Behavior**

| Field | Pointer | Kind |
| --- | --- | --- |
| Flavor | `/constraints/value/flavor` | select |

**Commerce (optional)**

| Field | Pointer | Kind |
| --- | --- | --- |
| Unlock SKU | `/businessCase/value/pricing/sku` | text |
| Price | `/businessCase/value/pricing/regularPrice` | text |
| Currency | `/businessCase/value/pricing/currency` | text |


---

### 🎯 Challenge — `challenge`

A short quiz with a personalized score and a shareable link.

- **Uses:** `metadata`, `productDescription`, `personas`, `constraints`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`


**Basics**

| Field | Pointer | Kind |
| --- | --- | --- |
| Challenge title | `/metadata/value/title` | text |
| One-line hook | `/productDescription/value/tagline` | text |
| Intro (shown before questions) | `/productDescription/value/description` | markdown |

**Audience**

| Field | Pointer | Kind |
| --- | --- | --- |
| Who it's for | `/personas/value/target_audience` | textarea |
| Languages | `/personas/value/languages` | chips |

**Sharing**

| Field | Pointer | Kind |
| --- | --- | --- |
| Share message template | `/constraints/value/share_title` | text |


---

### 📅 Event — `event`

A calendar event with a start and end.

- **Uses:** `metadata`, `productDescription`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`


**Event**

| Field | Pointer | Kind |
| --- | --- | --- |
| Event title | `/metadata/value/title` | text |
| Starts at (ISO) | `/metadata/value/start` | text |
| Ends at (ISO) | `/metadata/value/end` | text |
| Location | `/metadata/value/location` | text |
| Notes | `/productDescription/value/description` | markdown |


---

### 👥 Meeting — `meeting`

An event subtype with attendees and an agenda.

- **Uses:** `metadata`, `productDescription`, `acceptance`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`


**Meeting**

| Field | Pointer | Kind |
| --- | --- | --- |
| Meeting title | `/metadata/value/title` | text |
| Starts at (ISO) | `/metadata/value/start` | text |
| Duration | `/metadata/value/duration` | text |
| Location / link | `/metadata/value/location` | text |

**Agenda & outcome**

| Field | Pointer | Kind |
| --- | --- | --- |
| Agenda | `/productDescription/value/description` | markdown |
| Attendees | `/metadata/value/attendees` | chips |
| Desired outcome | `/acceptance/value/criteria` | chips |


---

### 📞 Call — `call`

A logged phone or video interaction.

- **Uses:** `metadata`, `productDescription`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`


**Call**

| Field | Pointer | Kind |
| --- | --- | --- |
| Subject | `/metadata/value/title` | text |
| When (ISO) | `/metadata/value/start` | text |
| Duration | `/metadata/value/duration` | text |
| With | `/metadata/value/counterpart` | text |
| Notes | `/productDescription/value/description` | markdown |


---

### 📊 Activity — `activity`

A generic timeline entry — anything worth remembering happened.

- **Uses:** `metadata`, `productDescription`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`


**Activity**

| Field | Pointer | Kind |
| --- | --- | --- |
| Title | `/metadata/value/title` | text |
| Kind | `/metadata/value/kind` | select |
| When (ISO) | `/metadata/value/occurred_at` | text |
| Detail | `/productDescription/value/description` | markdown |


---

### 📄 Doc — `doc`

A knowledge document with a markdown body.

- **Uses:** `metadata`, `productDescription`, `references`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`


**Doc**

| Field | Pointer | Kind |
| --- | --- | --- |
| Title | `/metadata/value/title` | text |
| Summary | `/productDescription/value/tagline` | text |
| Body (markdown) | `/productDescription/value/description` | markdown |

**References**

| Field | Pointer | Kind |
| --- | --- | --- |
| Related links | `/references/value/links` | chips |


---

### 🗒️ Note — `note`

A short user note.

- **Uses:** `metadata`, `productDescription`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`


**Note**

| Field | Pointer | Kind |
| --- | --- | --- |
| Title | `/metadata/value/title` | text |
| Note | `/productDescription/value/description` | markdown |


---

### 📎 File — `file`

A wrapper around a stored object — points at a storage bucket path.

- **Uses:** `metadata`, `productDescription`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`


**File**

| Field | Pointer | Kind |
| --- | --- | --- |
| File name | `/metadata/value/title` | text |
| Storage bucket | `/metadata/value/bucket` | text |
| Storage path | `/metadata/value/path` | text |
| MIME type | `/metadata/value/mime` | text |
| Size (bytes) | `/metadata/value/size_bytes` | number |
| Notes | `/productDescription/value/description` | markdown |


---

### 🏷️ Tag — `tag`

A canonical tag from your taxonomy.

- **Uses:** `metadata`, `productDescription`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`


**Tag**

| Field | Pointer | Kind |
| --- | --- | --- |
| Tag name | `/metadata/value/title` | text |
| Slug | `/metadata/value/slug` | text |
| Color | `/metadata/value/color` | text |
| What this tag means | `/productDescription/value/description` | textarea |


---

### 🏷️ Price — `price`

A catalog price: currency, amount, interval, and validity window.

- **Uses:** `metadata`, `productDescription`, `businessCase`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`


**Price**

| Field | Pointer | Kind |
| --- | --- | --- |
| Label | `/metadata/value/title` | text |
| SKU | `/metadata/value/sku` | text |
| Currency | `/metadata/value/currency` | text |
| Amount (cents) | `/metadata/value/amount_cents` | number |
| Interval | `/metadata/value/interval` | select |
| Valid from (ISO) | `/metadata/value/valid_from` | text |
| Valid to (ISO) | `/metadata/value/valid_to` | text |
| Notes | `/productDescription/value/description` | markdown |


---

### 📦 Billing Plan — `billing_plan`

A pricing plan grouping one or more prices + entitlements.

- **Uses:** `metadata`, `productDescription`, `businessCase`, `functionalRequirements`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`


**Plan**

| Field | Pointer | Kind |
| --- | --- | --- |
| Plan name | `/metadata/value/title` | text |
| Tier | `/metadata/value/tier` | select |
| One-line summary | `/productDescription/value/tagline` | text |
| What's included (markdown) | `/productDescription/value/description` | markdown |


---

### 🧾 Invoice — `invoice`

A billable invoice with lines, totals, and Draft→Sent→Paid state.

- **Uses:** `metadata`, `productDescription`, `businessCase`, `references`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`
- **Lifecycle:** `draft` → `sent` → `paid` → `void`

**Invoice**

| Field | Pointer | Kind |
| --- | --- | --- |
| Invoice # | `/metadata/value/title` | text |
| Status | `/metadata/value/status` | select |
| Currency | `/metadata/value/currency` | text |
| Total (cents) | `/metadata/value/total_cents` | number |
| Due at (ISO) | `/metadata/value/due_at` | text |
| Customer id | `/metadata/value/customer_id` | text |
| Notes / line items markdown | `/productDescription/value/description` | markdown |


---

### 💳 Payment — `payment`

A settled or attempted payment against an invoice or SKU.

- **Uses:** `metadata`, `productDescription`, `references`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`


**Payment**

| Field | Pointer | Kind |
| --- | --- | --- |
| Reference | `/metadata/value/title` | text |
| Provider | `/metadata/value/provider` | select |
| Provider id | `/metadata/value/provider_id` | text |
| Currency | `/metadata/value/currency` | text |
| Amount (cents) | `/metadata/value/amount_cents` | number |
| Status | `/metadata/value/status` | select |
| Invoice id | `/metadata/value/invoice_id` | text |
| Paid at (ISO) | `/metadata/value/paid_at` | text |


---

### 🔁 Subscription — `subscription`

A recurring plan against a price, with lifecycle state.

- **Uses:** `metadata`, `productDescription`, `businessCase`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`
- **Lifecycle:** `trialing` → `active` → `past_due` → `canceled` → `paused`

**Subscription**

| Field | Pointer | Kind |
| --- | --- | --- |
| Label | `/metadata/value/title` | text |
| Customer id | `/metadata/value/customer_id` | text |
| Price id | `/metadata/value/price_id` | text |
| Status | `/metadata/value/status` | select |
| Started at (ISO) | `/metadata/value/started_at` | text |
| Current period end (ISO) | `/metadata/value/current_period_end` | text |


---

### 🔑 License — `license`

A capability grant to an actor for a bundle, with optional expiry.

- **Uses:** `metadata`, `productDescription`, `constraints`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`


**License**

| Field | Pointer | Kind |
| --- | --- | --- |
| Label | `/metadata/value/title` | text |
| Bundle record id | `/metadata/value/bundle_id` | text |
| SKU / capability | `/metadata/value/sku` | text |
| Grantee (user id) | `/metadata/value/grantee_id` | text |
| Seats | `/metadata/value/seats` | number |
| Expires at (ISO) | `/metadata/value/expires_at` | text |


---

### 👛 Wallet — `wallet`

A credit balance for an actor. Ledger-backed elsewhere.

- **Uses:** `metadata`, `productDescription`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`


**Wallet**

| Field | Pointer | Kind |
| --- | --- | --- |
| Label | `/metadata/value/title` | text |
| Actor (user id) | `/metadata/value/actor_id` | text |
| Currency / unit | `/metadata/value/currency` | text |
| Balance | `/metadata/value/balance` | number |


---

### 💬 Conversation — `conversation`

A 1:1 or group conversation grouping threads and messages.

- **Uses:** `metadata`, `productDescription`, `personas`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`


**Conversation**

| Field | Pointer | Kind |
| --- | --- | --- |
| Subject | `/metadata/value/title` | text |
| Kind | `/metadata/value/kind` | select |
| One-line summary | `/productDescription/value/tagline` | text |


---

### 🧵 Thread — `thread`

A single topical thread inside a conversation or channel.

- **Uses:** `metadata`, `productDescription`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`


**Thread**

| Field | Pointer | Kind |
| --- | --- | --- |
| Title | `/metadata/value/title` | text |
| Parent (conversation/channel id) | `/metadata/value/parent_id` | text |
| Topic summary | `/productDescription/value/tagline` | text |


---

### 📣 Channel — `channel`

A named channel for broadcasting or group discussion.

- **Uses:** `metadata`, `productDescription`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`


**Channel**

| Field | Pointer | Kind |
| --- | --- | --- |
| Name | `/metadata/value/title` | text |
| Slug | `/metadata/value/slug` | text |
| Visibility | `/metadata/value/visibility` | select |
| Description | `/productDescription/value/description` | markdown |


---

### ✉️ Message — `message`

A single message inside a conversation, thread, or channel.

- **Uses:** `metadata`, `productDescription`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`
- **Lifecycle:** `draft` → `sent` → `delivered` → `read` → `failed`

**Message**

| Field | Pointer | Kind |
| --- | --- | --- |
| Subject | `/metadata/value/title` | text |
| Parent id (conversation/thread/channel) | `/metadata/value/parent_id` | text |
| Sender user id | `/metadata/value/sender_id` | text |
| Channel | `/metadata/value/channel` | select |
| Status | `/metadata/value/status` | select |
| Body (markdown) | `/productDescription/value/description` | markdown |


---

### 📧 Email — `email`

An outbound or inbound email with subject and body.

- **Uses:** `metadata`, `productDescription`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`
- **Lifecycle:** `draft` → `sent` → `delivered` → `read` → `bounced` → `failed`

**Email**

| Field | Pointer | Kind |
| --- | --- | --- |
| Subject | `/metadata/value/title` | text |
| From | `/metadata/value/from_addr` | text |
| To | `/metadata/value/to_addr` | text |
| CC | `/metadata/value/cc_addr` | text |
| Status | `/metadata/value/status` | select |
| Body (markdown or HTML) | `/productDescription/value/description` | markdown |


---

### 🔔 Notification — `notification`

A short alert for one recipient, delivered in-app or via a channel.

- **Uses:** `metadata`, `productDescription`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`
- **Lifecycle:** `pending` → `sent` → `read` → `dismissed` → `failed`

**Notification**

| Field | Pointer | Kind |
| --- | --- | --- |
| Title | `/metadata/value/title` | text |
| Recipient user id | `/metadata/value/recipient_id` | text |
| Channel | `/metadata/value/channel` | select |
| Status | `/metadata/value/status` | select |
| Body | `/productDescription/value/description` | textarea |


---

### 📡 Broadcast — `broadcast`

A one-to-many announcement fanned out to a channel or list.

- **Uses:** `metadata`, `productDescription`, `personas`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`


**Broadcast**

| Field | Pointer | Kind |
| --- | --- | --- |
| Subject | `/metadata/value/title` | text |
| Channel id | `/metadata/value/channel_id` | text |
| Audience tags | `/metadata/value/audience` | chips |
| Scheduled at (ISO) | `/metadata/value/scheduled_at` | text |
| Body (markdown) | `/productDescription/value/description` | markdown |


---

### 📥 Inbox — `inbox`

An owner's collection of incoming messages/notifications.

- **Uses:** `metadata`, `productDescription`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`


**Inbox**

| Field | Pointer | Kind |
| --- | --- | --- |
| Label | `/metadata/value/title` | text |
| Channels | `/metadata/value/channels` | chips |


---

### 📤 Outbox — `outbox`

An owner's queue of outgoing messages/broadcasts.

- **Uses:** `metadata`, `productDescription`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`


**Outbox**

| Field | Pointer | Kind |
| --- | --- | --- |
| Label | `/metadata/value/title` | text |
| Channels | `/metadata/value/channels` | chips |


---

### 🪝 Webhook — `webhook`

An outbound webhook endpoint receiving events for a record or channel.

- **Uses:** `metadata`, `productDescription`
- **Title from:** `/metadata/value/title`
- **Summary from:** `/productDescription/value/tagline`


**Webhook**

| Field | Pointer | Kind |
| --- | --- | --- |
| Label | `/metadata/value/title` | text |
| URL | `/metadata/value/url` | url |
| Subscribed events | `/metadata/value/events` | chips |
| Secret id (reference) | `/metadata/value/secret_id` | text |
| Active | `/metadata/value/active` | bool |

