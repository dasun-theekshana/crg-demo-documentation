# Settings

**Route:** `/settings`

User-level preferences for the CRM application.

## Data Model

```ts
interface Settings {
  id: string
  userId: string
  theme: 'light' | 'dark' | 'system'
  notifications: boolean
  currency: string    // e.g. "USD", "EUR"
  timezone: string    // e.g. "America/New_York"
  createdAt: string
  updatedAt: string
}
```

## Available Preferences

| Setting | Options | Default |
|---------|---------|---------|
| Theme | light / dark / system | system |
| Notifications | enabled / disabled | enabled |
| Currency | USD, EUR, GBP, etc. | USD |
| Timezone | IANA timezone string | UTC |

## API Calls

| Method | Endpoint | Purpose |
|--------|----------|---------|
| `GET` | `/api/settings/:userId` | Get settings for a user |
| `PUT` | `/api/settings/:userId` | Update all settings |
| `PATCH` | `/api/settings/:userId` | Partial update |
