# Dashboard

**Route:** `/`

The dashboard is the home page of the CRM, providing a high-level summary of business activity.

## Sections

### Stats Cards

Four top-level KPI cards:

| Card | Description |
|------|-------------|
| Total Contacts | Count of all contacts |
| Total Companies | Count of all companies |
| Total Deals | Count of all deals |
| Total Activities | Count of all activities |

### Pipeline Breakdown

Shows the count and total value of deals grouped by stage:

- Lead
- Qualified
- Proposal
- Negotiation
- Closed Won
- Closed Lost

### Win Rate

Calculated as: `closed-won deals / (closed-won + closed-lost deals) * 100`

### Recent Deals

A list of the most recently created deals with their stage, value, and associated company.

### Upcoming Activities

Activities with a due date in the future that are not yet completed, sorted by due date ascending.

## API Calls

| Method | Endpoint | Purpose |
|--------|----------|---------|
| `GET` | `/api/dashboard` | Fetches all summary stats in a single call |
