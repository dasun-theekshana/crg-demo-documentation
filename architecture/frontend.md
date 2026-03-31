# Frontend Architecture

## Stack

| Tool | Version | Purpose |
|------|---------|---------|
| React | 19.x | UI framework |
| React Router | 7.x | Client-side routing |
| Vite | 7.x | Build tool + dev server |
| TailwindCSS | 4.x | Utility-first CSS |
| TypeScript | 5.x | Type safety |
| Lucide React | latest | Icon library |

## Directory Structure

```
crm/src/
├── main.tsx          # App entry point, CRG provider setup
├── App.tsx           # Router configuration
├── index.css         # Global Tailwind imports
├── api/              # API client modules
├── components/       # Reusable UI components
├── layouts/          # Page layout wrappers
├── pages/            # Route-level page components
├── types/            # TypeScript interfaces
└── data/             # Static seed JSON (unused at runtime)
```

## Entry Point (`main.tsx`)

The entry point conditionally wraps the app with `CRGProvider` based on the `VITE_CRG_ENABLED` environment variable. When CRG is enabled, it also mounts the Sidecar UI and Assist UI portals.

```tsx
// Simplified structure
if (CRG_ENABLED) {
  <CRGProvider config={crgConfig}>
    <App />
    <SidecarUI />
    <AssistUI />
  </CRGProvider>
} else {
  <App />
}
```

## Routing (`App.tsx`)

Uses React Router v7 with a nested layout pattern:

```
/                   → AppLayout (sidebar + header shell)
├── /               → Dashboard
├── /contacts       → Contacts
├── /companies      → Companies
├── /deals          → Deals
├── /activities     → Activities
└── /settings       → Settings
```

## Layout (`AppLayout.tsx`)

A fixed two-column layout:

- **Sidebar (264px):** Dark slate-900 background with logo, nav links, and user section
- **Main area:** Full-width content area with a top header bar

## API Layer (`api/`)

All data fetching is handled through a singleton `ApiClient` class:

```ts
// crm/src/api/client.ts
class ApiClient {
  async get<T>(path: string): Promise<T>
  async post<T>(path: string, body: unknown): Promise<T>
  async put<T>(path: string, body: unknown): Promise<T>
  async patch<T>(path: string, body: unknown): Promise<T>
  async delete<T>(path: string): Promise<T>
}
```

Each domain has its own module (`contacts.ts`, `companies.ts`, etc.) that calls `ApiClient` with typed return values.

!!! info "CRG Probe Logging"
    `ApiClient` logs every request to `console.log` so the CRG probe can intercept and learn API call patterns.

## Component Library (`components/`)

Reusable, unstyled-but-themed components:

| Component | Purpose |
|-----------|---------|
| `Button` | Primary/secondary/danger variants |
| `Input` | Text input with label and error state |
| `Select` | Dropdown select |
| `Badge` | Status and label badges |
| `Card` | Content card wrapper |
| `DataTable` | Sortable, filterable table |
| `Modal` | Dialog overlay |
| `ContactModal` | Create/edit contact form |
| `CompanyModal` | Create/edit company form |
| `DealModal` | Create/edit deal form |
| `ActivityModal` | Create/edit activity form |

## TypeScript Types (`types/index.ts`)

Core domain models:

```ts
Contact   { id, firstName, lastName, email, phone, companyId, title, status, ... }
Company   { id, name, industry, website, size, address, parentId, ... }
Deal      { id, title, value, currency, stage, probability, contactId, companyId, ... }
Activity  { id, type, subject, description, contactId, companyId, dealId, dueDate, ... }
Settings  { id, userId, theme, notifications, currency, timezone, ... }
User      { id, name, email, avatar, role }
```
