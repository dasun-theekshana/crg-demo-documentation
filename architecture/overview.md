# Architecture Overview

The application is a **monorepo** containing two packages managed as npm workspaces.

## High-Level Diagram

```
┌─────────────────────────────────────────────────┐
│                  Browser                         │
│                                                  │
│  ┌──────────────────────────────────────────┐   │
│  │           React SPA (port 5173)          │   │
│  │                                          │   │
│  │  ┌──────────────┐  ┌──────────────────┐  │   │
│  │  │  CRG Sidecar │  │   CRM App        │  │   │
│  │  │  + Assist UI │  │   (Router+Pages) │  │   │
│  │  └──────────────┘  └──────────────────┘  │   │
│  │                           │               │   │
│  │                      ApiClient           │   │
│  └───────────────────────────┼───────────────┘   │
└──────────────────────────────┼───────────────────┘
                               │ /api/* (proxy in dev)
                               ▼
┌──────────────────────────────────────────────────┐
│           Hono API Server (port 8787)            │
│                                                  │
│   /contacts  /companies  /deals  /activities     │
│   /settings  /dashboard                         │
│                                                  │
│   ┌─────────────────────────────────────────┐   │
│   │           In-Memory Data Store          │   │
│   └─────────────────────────────────────────┘   │
└──────────────────────────────────────────────────┘
```

## Packages

### `crm` — React Frontend

- Entry point: `crm/src/main.tsx`
- Built with Vite, deployed as a static site
- Communicates with the API via the `ApiClient` singleton
- Conditionally mounts CRG provider and UI components based on `VITE_CRG_ENABLED`

### `crm-api` — Hono Backend

- Entry point: `crm-api/src/index.ts`
- Runs on Node.js locally (`node.ts`) or Cloudflare Workers in production
- Uses an in-memory store seeded with demo data on first request
- Exposes a REST API consumed by the frontend

## Data Flow

1. User navigates to a page in the CRM
2. The page component calls an API module (e.g., `contacts.ts`)
3. The API module calls `ApiClient`, which logs the request and fetches from `/api/...`
4. Vite proxies the request to the Hono server
5. The Hono route reads/writes the in-memory store and returns JSON
6. The page re-renders with the new data

!!! note "Demo Data"
    The in-memory store is seeded from `crm-api/src/db/seed-data.ts` on startup. All data resets when the server restarts.
