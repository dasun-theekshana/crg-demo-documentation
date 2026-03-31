# Deals

**Route:** `/deals`

Track sales opportunities through a defined pipeline.

## Data Model

```ts
interface Deal {
  id: string
  title: string
  value: number
  currency: string           // e.g. "USD"
  stage: DealStage
  probability: number        // 0-100 percentage
  contactId: string
  companyId: string
  expectedCloseDate: string  // ISO date string
  notes: string
  createdAt: string
  updatedAt: string
}

type DealStage =
  | 'lead'
  | 'qualified'
  | 'proposal'
  | 'negotiation'
  | 'closed-won'
  | 'closed-lost'
```

## Pipeline Stages

```
lead → qualified → proposal → negotiation → closed-won
                                          ↘ closed-lost
```

| Stage | Description |
|-------|-------------|
| `lead` | Initial interest, unqualified |
| `qualified` | Budget and need confirmed |
| `proposal` | Formal proposal sent |
| `negotiation` | Terms being negotiated |
| `closed-won` | Deal won |
| `closed-lost` | Deal lost |

## Features

- **List view** with pipeline stage breakdown
- **Filter by stage** — view deals within a specific stage
- **Create / edit / delete** via `DealModal`
- **Probability tracking** — manual probability estimate per deal
- **Value and currency** — multi-currency display support

## API Calls

| Method | Endpoint | Purpose |
|--------|----------|---------|
| `GET` | `/api/deals` | List all deals |
| `POST` | `/api/deals` | Create a deal |
| `PUT` | `/api/deals/:id` | Update a deal |
| `DELETE` | `/api/deals/:id` | Delete a deal |
