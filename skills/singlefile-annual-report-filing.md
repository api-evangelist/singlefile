---
name: File an annual report with SingleFile
description: Find entities with upcoming annual-report tasks and file the report to keep them in good standing.
api: openapi/singlefile-openapi.yml
operations: [entities_list_list, entities_tasks_list, entities_jurisdictions_list, schemas_read, create_order, place_order, get_order]
generated: '2026-07-21'
method: generated
---

# File an annual report

## Auth
OAuth 2.0 client credentials (see the formation skill). Base URL `https://api.demo.singlefile.ai/external-api/v1`.

## Steps
1. `entities_list_list` — enumerate entities (paginate with `page_number`/`page_size`).
2. `entities_tasks_list` — for each entity, list compliance tasks and find due/upcoming annual-report deadlines.
3. `entities_jurisdictions_list` — confirm the jurisdiction the report is due in.
4. `schemas_read` — get the order-payload schema for `filing_type=annual_report` in that jurisdiction.
5. `create_order` — create the annual-report order.
6. `place_order` — submit it.
7. `get_order` — confirm completion (or subscribe to `order.completed`).

## Notes
- Watch the `task.created` webhook to react to newly-generated compliance deadlines in real time.
- Error envelope: `{success:false, error:{code,message,validation_errors}}`.
