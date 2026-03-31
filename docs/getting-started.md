# Getting Started

## Prerequisites

- **Node.js** 20+ (see `.nvmrc`)
- **npm** 10+ or **pnpm**

```bash
# Using nvm (recommended)
nvm use
```

## Installation

Clone the repository and install dependencies from the root:

```bash
npm install
```

This installs dependencies for both the `crm` and `crm-api` workspaces.

## Running in Development

Start both the frontend and API server concurrently:

```bash
npm run dev
```

| Service | URL |
|---------|-----|
| Frontend | http://localhost:5173 |
| API | http://localhost:8787 |

The frontend's Vite dev server proxies all `/api/*` requests to the API at port 8787.

## Environment Variables

The frontend reads CRG configuration from `crm/.env`:

```env
VITE_CRG_ENABLED=true
VITE_CRG_APP_ID=crm-demo
VITE_CRG_SERVICE_URL=http://localhost:3001
VITE_CRG_GRAPH_SERVICE_URL=http://localhost:8002
VITE_CRG_SOURCE_CODE_PATH=C:\path\to\source
```

To disable CRG integration locally, set `VITE_CRG_ENABLED=false`.

## Building for Production

```bash
npm run build
```

Builds both the React app (output: `crm/dist/`) and the Cloudflare Worker bundle.

## Available Scripts

| Script | Description |
|--------|-------------|
| `npm run dev` | Start frontend + API in watch mode |
| `npm run build` | Build both apps for production |
| `npm run test` | Run all tests |
| `npm run lint` | Lint the frontend source |
