# Testing

Both the frontend and backend use [Vitest](https://vitest.dev/) as the test runner.

## Running Tests

```bash
# All tests (root)
npm run test

# Frontend tests only
cd crm && npm run test

# API tests only
cd crm-api && npm run test
```

## Test Coverage

| Package | Test Count | Coverage Area |
|---------|-----------|---------------|
| `crm-api` | ~115 tests | All route handlers and business logic |
| `crm` | ~10 tests | API client module |

## Backend Tests (`crm-api`)

Tests are co-located with source files or in a `__tests__` directory. They test:

- **Route handlers** — HTTP status codes, response shapes, error cases
- **Data store** — CRUD operations, computed fields (contactCount, totalDealValue)
- **Seed data** — Data integrity and relationships

Each resource has its own test file matching the route file (e.g., `contacts.test.ts`).

## Frontend Tests (`crm`)

Frontend tests focus on the `ApiClient`:

- Correct URL construction
- Request serialization
- Error handling and response parsing
- Console logging behavior (for CRG probe interception)

## Test Configuration

Both packages use `vitest.config.ts` at their package root. The frontend tests run in a `jsdom` environment to simulate the browser.

```ts
// crm/vitest.config.ts (simplified)
export default defineConfig({
  test: {
    environment: 'jsdom',
  },
})
```

## Writing New Tests

For backend routes, follow the existing pattern:

```ts
import { describe, it, expect, beforeEach } from 'vitest'
import app from '../index'

describe('GET /api/contacts', () => {
  it('returns a list of contacts', async () => {
    const res = await app.request('/api/contacts')
    expect(res.status).toBe(200)
    const body = await res.json()
    expect(Array.isArray(body)).toBe(true)
  })
})
```
