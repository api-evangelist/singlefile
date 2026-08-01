---
name: File for an EIN with SingleFile
description: Obtain a federal Employer Identification Number for an existing entity via an EIN filing order.
api: openapi/singlefile-openapi.yml
operations: [entities_list_list, entities_read, schemas_read, create_order, place_order, get_order, entities_documents_list]
generated: '2026-07-21'
method: generated
---

# File for an EIN

## Auth
OAuth 2.0 client credentials (see the formation skill). Base URL `https://api.demo.singlefile.ai/external-api/v1`.

## Steps
1. `entities_list_list` / `entities_read` — locate the entity that needs an EIN and confirm its details.
2. `schemas_read` — retrieve the order-payload schema for `filing_type=ein` in the entity's jurisdiction.
3. `create_order` — create the EIN filing order.
4. `place_order` — submit it.
5. `get_order` — poll for completion (or handle the `order.completed` webhook).
6. `entities_documents_list` — once complete, list the entity's documents to retrieve the EIN confirmation.

## Notes
- Rate limits: 1000 req/hour, 60 req/minute burst.
- Errors follow the `{success, error}` envelope; on `NOT_FOUND` re-verify the entity id.
