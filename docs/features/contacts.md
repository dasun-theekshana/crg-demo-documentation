# Contacts

**Route:** `/contacts`

Manage individual people (leads, customers, prospects) in the CRM.

## Data Model

```ts
interface Contact {
  id: string
  firstName: string
  lastName: string
  email: string
  phone: string
  companyId: string       // Foreign key to Company
  title: string           // Job title
  status: 'active' | 'inactive' | 'lead'
  createdAt: string       // ISO date string
  updatedAt: string
}
```

## Features

- **List view** with sortable columns via `DataTable`
- **Search** by name or email (client-side filter)
- **Filter by status** (active / inactive / lead)
- **Create** new contact via `ContactModal`
- **Edit** existing contact inline
- **Delete** contact with confirmation

## Status Meanings

| Status | Meaning |
|--------|---------|
| `active` | Current customer or active relationship |
| `lead` | Prospect not yet converted |
| `inactive` | Former contact, no current relationship |

## API Calls

| Method | Endpoint | Purpose |
|--------|----------|---------|
| `GET` | `/api/contacts` | List all contacts |
| `POST` | `/api/contacts` | Create a contact |
| `PUT` | `/api/contacts/:id` | Update a contact |
| `DELETE` | `/api/contacts/:id` | Delete a contact |
