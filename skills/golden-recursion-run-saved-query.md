---
name: Run a saved Golden query
description: Pull the results of a saved Golden Query Tool query by ID or permalink into your own workflow.
api: openapi/golden-recursion-openapi-original.json
operations: [public_api_queries_results_list, public_api_queries_permalink_list]
generated: '2026-07-19'
method: generated
---

# Run a saved Golden query

Fetch the entity results of a query you built in the Golden Query Tool, straight over the API.

## Auth
Header `apikey: <YOUR_KEY>`. Base URL: `https://golden.com/api/v2/public`.

## Steps
1. **By query ID** — call `public_api_queries_results_list` (`GET /api/v2/public/queries/{id}/results/`) with the numeric query `id` from the Query Tool.
2. **By permalink** — alternatively call `public_api_queries_permalink_list` (`GET /api/v2/public/queries/permalink/{permalink}/`) using the query's shareable permalink.
3. **Page through results** — both return cursor-paginated entity lists; follow `next` until null and collect `results[]`.
4. **Keep data fresh** — re-run on a schedule to keep an internal dataset in sync; every value stays cited.

## Conventions & errors
- Cursor pagination and the DRF error envelope apply — see `conventions/golden-recursion-conventions.yml` and `errors/golden-recursion-problem-types.yml`.
