# Changelog

## 2.0.0 — 2026-08-17

Full rewrite, generated from the reference implementation. Replaces the initial
Copilot draft.

- Components, entities, capabilities and state machines are now generated from
  the live registry, so spec and implementation cannot drift.
- Added `pbx_ext`: typed, versioned domain extensions with registered kinds.
- Added JSON Pointer addressing as the canonical way to reference fields.
- Added typed links (`from`, `to`, `role`, `weight`) and graph semantics.
- Added embed aspects mapping components to named vectors.
- Added integration guides: MCP, embed script, WordPress/WooCommerce, registry
  endpoint.
- Added JSON Schemas and one example document per core entity.

## 0.1.0

Initial draft.
