---
name: Manage entity documents with SingleFile
description: Upload supporting documents to an entity or organization, then list and download compliance records.
api: openapi/singlefile-openapi.yml
operations: [entities_documents_upload_create, entities_documents_list, organizations_documents_upload_create, organizations_documents_list, documents_read]
generated: '2026-07-21'
method: generated
---

# Manage documents

## Auth
OAuth 2.0 client credentials (see the formation skill). Base URL `https://api.demo.singlefile.ai/external-api/v1`.

## Steps
1. `entities_documents_upload_create` (or `organizations_documents_upload_create`) — upload a supporting document. Supported types: PDF, JPG/JPEG/PNG/GIF, DOC/DOCX. Max 10MB, one attachment per order.
2. `entities_documents_list` (or `organizations_documents_list`) — list documents attached to the entity/organization.
3. `documents_read` — retrieve a specific document's detail/download reference.

## Notes
- Uploaded documents can reduce the number of required fields in order payloads by supplying supporting data.
- React to `document.created` / `document.updated` / `document.deleted` webhooks to keep a local mirror in sync.
- Errors use the `{success, error}` envelope.
