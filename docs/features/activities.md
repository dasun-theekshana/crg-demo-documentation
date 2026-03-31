# Activities

**Route:** `/activities`

Log and track interactions and tasks related to contacts, companies, and deals.

## Data Model

```ts
interface Activity {
  id: string
  type: ActivityType
  subject: string
  description: string
  contactId: string | null
  companyId: string | null
  dealId: string | null
  dueDate: string          // ISO date string
  completed: boolean
  createdAt: string
  updatedAt: string
}

type ActivityType = 'call' | 'email' | 'meeting' | 'task' | 'note'
```

## Activity Types

| Type | Description |
|------|-------------|
| `call` | Phone or video call |
| `email` | Email correspondence |
| `meeting` | In-person or virtual meeting |
| `task` | To-do item or follow-up action |
| `note` | Free-form note about a contact/deal |

## Features

- **List view** with type icons and due dates
- **Filter by type** and **completion status**
- **Create / edit / delete** via `ActivityModal`
- **Due date tracking** — overdue activities are highlighted
- **Mark as complete** — toggle completion inline
- Activities can be linked to a contact, company, and/or deal simultaneously

## API Calls

| Method | Endpoint | Purpose |
|--------|----------|---------|
| `GET` | `/api/activities` | List all activities |
| `POST` | `/api/activities` | Create an activity |
| `PUT` | `/api/activities/:id` | Update an activity |
| `PATCH` | `/api/activities/:id` | Partial update (e.g., toggle completed) |
| `DELETE` | `/api/activities/:id` | Delete an activity |
