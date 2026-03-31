# Development Setup

## Prerequisites

- Node.js 20+ (`nvm use` if you have nvm)
- npm 10+

## First-Time Setup

```bash
# From the repo root
npm install
```

This installs all workspace dependencies for both `crm` and `crm-api`.

## Starting the Dev Environment

```bash
npm run dev
```

This concurrently starts:

1. **Vite dev server** (`crm`) → http://localhost:5173 with HMR
2. **Hono Node.js server** (`crm-api`) → http://localhost:8787

The Vite config proxies `/api/*` to `http://localhost:8787`, so you can use relative `/api/...` paths in the frontend.

## Running Individual Services

```bash
# Frontend only
cd crm && npm run dev

# API only
cd crm-api && npm run dev
```

## Environment Setup

Copy and edit the frontend environment file:

```bash
cp crm/.env.example crm/.env
# Edit .env to set CRG service URLs and toggle VITE_CRG_ENABLED
```

## Linting

```bash
npm run lint
# Runs ESLint on crm/src/**
```

## Building

```bash
npm run build
# Produces crm/dist/ and crm-api/dist/
```

## Useful Paths

| Path | Description |
|------|-------------|
| `crm/src/main.tsx` | Frontend entry point |
| `crm/src/App.tsx` | Router and route definitions |
| `crm-api/src/index.ts` | API entry point |
| `crm-api/src/db/store.ts` | In-memory data store |
| `crm-api/src/db/seed-data.ts` | Demo seed data |
| `crm/.env` | Frontend environment variables |
| `crm/vite.config.ts` | Vite config including dev proxy |
