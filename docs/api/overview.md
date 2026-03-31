# API Overview

The CRM API is a REST API built with [Hono](https://hono.dev/) served under the `/api` prefix.

## Base URL

| Environment | URL |
|-------------|-----|
| Development | `http://localhost:8787/api` |
| Frontend proxy | `http://localhost:5173/api` (proxied to 8787) |
| Production | Cloudflare Worker URL |

## Common Conventions

### Request Format

All write operations accept `application/json` body:

```http
POST /api/contacts
Content-Type: application/json

{
  "firstName": "Jane",
  "lastName": "Smith",
  "email": "jane@example.com"
}
```

### Response Format

All responses return JSON. Lists return arrays; single resources return objects:

```json
// List
[{ "id": "1", ... }, { "id": "2", ... }]

// Single
{ "id": "1", "firstName": "Jane", ... }
```

### Error Responses

```json
{
  "error": "Not found",
  "status": 404
}
```

### IDs

All record IDs are strings (UUID v4 format generated server-side).

### Dates

All date fields are ISO 8601 strings: `"2025-01-15T10:30:00.000Z"`

## CORS

The API sets permissive CORS headers for local development. Production deployments should restrict the `Origin` header.

## Resources

| Resource | Base Path |
|----------|-----------|
| Contacts | `/api/contacts` |
| Companies | `/api/companies` |
| Deals | `/api/deals` |
| Activities | `/api/activities` |
| Settings | `/api/settings` |
| Dashboard | `/api/dashboard` |
