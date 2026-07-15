# Product Data Enrichment Standard — Prototype

This repository contains a first-draft prototype of a product-data field specification. This is a fields/specification document only; it is not an API and does not define an implementation.

Goal

Provide better context with product data for improved positioning in product search

Problem

Product data (like WooCommerce product data) is too thin for an LLM to position the product correctly.

Current product listings often only capture the "what" (title and short description). This standard is derived from a Prince2 style Project Brief, that answers 'who, what, where, when, why'.

Apart from 'standard' product data, size, weight, color, you also specify the goal, the problem it solves, example users, example use cases. Especially when working with vectors, that gives an AI a lot more handles to position the proposal/product.

This specification documents field names and modules for product data enrichment. 

Modules (files present in this repository)

- acceptance.json
- ai-metadata.json
- assumptions.json
- business-case.json
- business-processes.json
- common.json
- constraints.json
- decisions.json
- dependencies.json
- embeddings_mapping.json
- functional-requirements.json
- glossary.json
- governance.json
- interfaces.json
- metadata.json
- non-functional-requirements.json
- open-questions.json
- opportunities.json
- outcomes.json
- personas.json
- problem-domain.json
- product-description.json
- project-brief-schema-expanded-full.json
- project-brief-schema.json
- project-definition.json
- quality.json
- references.json
- risks.json
- scope.json
- solution-options.json
- stakeholders.json
- success-metrics.json
- technology-considerations.json
- users.json

(each with an '.expanded.json' extension)

Contributing

This is a prototype. Please:

    Open issues for proposals and edge cases.
    Submit PRs for schema changes or examples.

Roadmap (short)

    Stabilize core fields and types.
    Test standard on openideabox.com

License

This repository is licensed under the GNU General Public License v3.0 (GPL-3.0). See the `LICENSE` file for the full text.
