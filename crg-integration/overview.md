# CRG Integration Overview

CRG (Conversational Product Intelligence) is a platform that enables users to interact with web applications through natural language. This CRM is a **host application** — it embeds the CRG connector to allow CRG to learn and assist within the CRM.

## What CRG Provides

| Component | Description |
|-----------|-------------|
| **CRGProvider** | React context provider that initializes the CRG session |
| **Sidecar UI** | A sidebar panel for human feedback during probe training |
| **Assist UI** | The primary conversational interface for end users |
| **Background Capture** | Automatic DOM snapshot collection for probe training |
| **Probe** | CRG's backend system that builds a graph of the app |

## Integration Points

### 1. React Provider (`main.tsx`)

The entire React app is wrapped in `CRGProvider` when `VITE_CRG_ENABLED=true`. This gives CRG access to the React component tree and routing context.

### 2. API Logging (`api/client.ts`)

Every API call is logged to `console.log` before it is made. CRG's probe intercepts these logs to learn what data the app fetches and when.

### 3. Background Capture

The CRG connector automatically captures DOM snapshots with configurable debouncing:

- **Debounce interval:** 1000ms
- **Mutation tracking:** Enabled
- **Content hashing:** Enabled (deduplicates identical snapshots)
- **Mutation threshold:** 10 DOM changes before triggering a capture

### 4. Sitemap Metadata

The `crm-sitemap.json` file provides a structured map of all routes, sections, interactive elements, and data flows for CRG to bootstrap its understanding of the app without requiring full probe training.

## CRG Packages

| Package | Purpose |
|---------|---------|
| `@crg/connector-react` | React-specific integration (CRGProvider, hooks) |
| `@crg/connector-core` | Platform-agnostic core connector logic |
| `@crg/sidecar-ui` | Sidecar UI component for human feedback |

These packages are referenced as local file paths in `crm/package.json`, meaning they are developed alongside this host app.
