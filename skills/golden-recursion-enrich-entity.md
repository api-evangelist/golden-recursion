---
name: Enrich an entity from Golden
description: Look up a company, person or VC in the Golden knowledge graph and pull its cited, structured properties.
api: openapi/golden-recursion-openapi-original.json
operations: [public_api_entities_list, public_api_entities_retrieve, public_api_schema_predicates_list]
generated: '2026-07-19'
method: generated
---

# Enrich an entity from Golden

Use the Golden API v2 to find an entity and retrieve its cited properties. The API is read-only and authenticated with an `apikey` header.

## Auth
Send every request with header `apikey: <YOUR_KEY>` (get a key from the Golden API Settings page). Base URL: `https://golden.com/api/v2/public`.

## Steps
1. **Find candidates** — call `public_api_entities_list` (`GET /api/v2/public/entities/`). Narrow with `entityTypeIds` (e.g. `6` company, `36` person) and project properties with `predicateIds`. Page with `cursor` + `pageSize`; follow the `next` URL until null.
2. **Discover predicate IDs** — if you need specific fields, call `public_api_schema_predicates_list` (`GET /api/v2/public/schema/predicates/`) to map predicate names to IDs, and note which are `isFilterable`.
3. **Retrieve the full entity** — call `public_api_entities_retrieve` (`GET /api/v2/public/entities/{id}/`) with the entity `id` to get its complete `properties[]`.
4. **Trace values** — each property value carries `citations` (title + url); surface them so the enriched data is auditable.

## Conventions & errors
- Pagination is cursor-based (`next`/`previous` URLs). See `conventions/golden-recursion-conventions.yml`.
- Errors use a DRF envelope `{type, errors:[{code, detail, attr}]}`; handle `403 permission_denied`, `404 not_found`, `429 throttled`. See `errors/golden-recursion-problem-types.yml`.
