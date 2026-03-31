# Backend Architecture

## Stack

| Tool | Version | Purpose |
|------|---------|---------|
| Hono | 4.x | Lightweight web framework |
| @hono/node-server | 1.x | Node.js adapter for local dev |
| Wrangler | 3.x | Cloudflare Workers CLI |
| TypeScript | 5.x | Type safety |
| Vitest | latest | Testing framework |

## Directory Structure

```
crm-api/src/
├── index.ts          # Hono app entry point, route registration
├── node.ts           # Node.js dev server wrapper
├── routes/
│   ├── contacts.ts
│   ├── companies.ts
│   ├── deals.ts
│   ├── activities.ts
│   ├── dashboard.ts
│   └── settings.ts
└── db/
    ├── store.ts      # In-memory data store with CRUD helpers
    ├── seed-data.ts  # Demo seed data
    └── types.ts      # Data type definitions
```

## App Entry Point (`index.ts`)

The Hono app registers all route modules under the `/api` prefix and sets CORS headers for local development:

```ts
const app = new Hono()
app.use('/api/*', cors())
app.route('/api/contacts', contactsRoutes)
app.route('/api/companies', companiesRoutes)
// ... etc
export default app
```

## In-Memory Store (`db/store.ts`)

The store holds all data in plain arrays. It is seeded on first access from `seed-data.ts`. All operations are synchronous.

```ts
// Simplified interface
const store = {
  contacts: Contact[],
  companies: Company[],
  deals: Deal[],
  activities: Activity[],
  settings: Settings[],
}
```

!!! warning "Data Persistence"
    This is a demo application. All data is stored in memory and **resets on every server restart**. It is not suitable for production use.

## Deployment

### Local Development

```bash
cd crm-api
npm run dev
# Starts @hono/node-server on port 8787
```

### Cloudflare Workers (Production)

The same `index.ts` is compatible with the Cloudflare Workers runtime via `wrangler.toml`:

```bash
cd crm-api
npx wrangler deploy
```

The `export default app` pattern works for both runtimes without code changes.
