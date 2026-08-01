---
name: Form a business entity with SingleFile
description: Create an organization and entity, attach a jurisdiction, then create and place a formation order.
api: openapi/singlefile-openapi.yml
operations: [organizations_create_create, organizations_entity_create_create, entities_jurisdictions_create_create, schemas_read, create_order, place_order, get_order]
generated: '2026-07-21'
method: generated
---

# Form a business entity

Automate LLC / Corporation formation across US jurisdictions.

## Auth
OAuth 2.0 client credentials. `POST https://api.demo.singlefile.ai/o/token/` with `grant_type=client_credentials`, `client_id`, `client_secret`; use the returned bearer token (valid 3600s) as `Authorization: Bearer <token>` on every call. Base URL: `https://api.demo.singlefile.ai/external-api/v1`.

## Steps
1. `organizations_create_create` — create the owning organization (or reuse an existing one via `organizations_list_list`).
2. `organizations_entity_create_create` — create the entity under that organization.
3. `entities_jurisdictions_create_create` — add the formation jurisdiction (state) to the entity.
4. `schemas_read` — fetch the JSON schema for the order payload for this `entity_type` / `filing_type` / `jurisdiction` so you send the right fields.
5. `create_order` — create the formation order using the schema.
6. `place_order` — submit the order for processing.
7. `get_order` — poll order status, or subscribe to the `order.completed` webhook.

## Conventions
- Pagination on list calls: `page_number` / `page_size`; response has `count`/`next`/`previous`/`results`.
- Errors: `{success:false, error:{code,message,validation_errors}}` — inspect `validation_errors` on `VALIDATION_ERROR`.
- No REST idempotency key; do not blindly retry `place_order`. Use `get_order` to confirm state before retrying.
