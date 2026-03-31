# Companies

**Route:** `/companies`

Manage organizations — customers, prospects, or partners.

## Data Model

```ts
interface Company {
  id: string
  name: string
  industry: string
  website: string
  size: string             // e.g. "1-10", "11-50", "51-200", "201-500", "500+"
  address: string
  parentId: string | null  // Subsidiary relationship
  contactCount: number     // Computed
  totalDealValue: number   // Computed
  createdAt: string
}
```

## Features

- **List view** with search and sort
- **Industry filter**
- **Hierarchical relationships** — a company can have a `parentId` pointing to another company (subsidiary/parent structure)
- **Create / edit / delete** via `CompanyModal`
- **Computed fields** — `contactCount` and `totalDealValue` are derived server-side from related records

## API Calls

| Method | Endpoint | Purpose |
|--------|----------|---------|
| `GET` | `/api/companies` | List all companies |
| `POST` | `/api/companies` | Create a company |
| `PUT` | `/api/companies/:id` | Update a company |
| `DELETE` | `/api/companies/:id` | Delete a company |
