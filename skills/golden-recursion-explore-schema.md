---
name: Explore the Golden schema
description: Introspect Golden's entity types and predicates so you can build correct filters and property projections.
api: openapi/golden-recursion-openapi-original.json
operations: [public_api_schema_entityTypes_list, public_api_schema_entityTypes_retrieve, public_api_schema_predicates_list, public_api_schema_predicates_retrieve]
generated: '2026-07-19'
method: generated
---

# Explore the Golden schema

Before querying entities, introspect the graph's shape: which entity types exist and which predicates (properties) they carry.

## Auth
Header `apikey: <YOUR_KEY>`. Base URL: `https://golden.com/api/v2/public`.

## Steps
1. **List entity types** — call `public_api_schema_entityTypes_list` (`GET /api/v2/public/schema/entityTypes/`) to get entity-type IDs (e.g. Company, Person) for use as `entityTypeIds`.
2. **Inspect one type** — call `public_api_schema_entityTypes_retrieve` (`GET /api/v2/public/schema/entityTypes/{id}/`) to see the predicates attached to that type.
3. **List predicates** — call `public_api_schema_predicates_list` (`GET /api/v2/public/schema/predicates/`) to map predicate names to IDs, their value `type` (int, text, url, entity, location, json…), and whether they are `isFilterable`.
4. **Inspect one predicate** — call `public_api_schema_predicates_retrieve` (`GET /api/v2/public/schema/predicates/{id}/`) for object choices, allowed entity types, or JSON subpredicates.
5. **Apply** — use the discovered IDs as `entityTypeIds`, `predicateIds`, and `filterPredicateId` when calling the Entity/Query APIs.

## Conventions & errors
- See `conventions/golden-recursion-conventions.yml` and `errors/golden-recursion-problem-types.yml`.
