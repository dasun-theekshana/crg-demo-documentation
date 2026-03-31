# API Endpoints

## Contacts

### `GET /api/contacts`
Returns all contacts.

**Response:** `Contact[]`

---

### `POST /api/contacts`
Creates a new contact.

**Body:**
```json
{
  "firstName": "string",
  "lastName": "string",
  "email": "string",
  "phone": "string",
  "companyId": "string",
  "title": "string",
  "status": "active | inactive | lead"
}
```

**Response:** `Contact`

---

### `PUT /api/contacts/:id`
Replaces a contact.

**Response:** `Contact`

---

### `DELETE /api/contacts/:id`
Deletes a contact.

**Response:** `204 No Content`

---

## Companies

### `GET /api/companies`
Returns all companies with computed `contactCount` and `totalDealValue`.

**Response:** `Company[]`

---

### `POST /api/companies`
Creates a new company.

**Body:**
```json
{
  "name": "string",
  "industry": "string",
  "website": "string",
  "size": "string",
  "address": "string",
  "parentId": "string | null"
}
```

**Response:** `Company`

---

### `PUT /api/companies/:id`
Replaces a company.

**Response:** `Company`

---

### `DELETE /api/companies/:id`
Deletes a company.

**Response:** `204 No Content`

---

## Deals

### `GET /api/deals`
Returns all deals.

**Response:** `Deal[]`

---

### `POST /api/deals`
Creates a new deal.

**Body:**
```json
{
  "title": "string",
  "value": 0,
  "currency": "USD",
  "stage": "lead | qualified | proposal | negotiation | closed-won | closed-lost",
  "probability": 0,
  "contactId": "string",
  "companyId": "string",
  "expectedCloseDate": "ISO date string",
  "notes": "string"
}
```

**Response:** `Deal`

---

### `PUT /api/deals/:id`
Replaces a deal.

**Response:** `Deal`

---

### `DELETE /api/deals/:id`
Deletes a deal.

**Response:** `204 No Content`

---

## Activities

### `GET /api/activities`
Returns all activities.

**Response:** `Activity[]`

---

### `POST /api/activities`
Creates a new activity.

**Body:**
```json
{
  "type": "call | email | meeting | task | note",
  "subject": "string",
  "description": "string",
  "contactId": "string | null",
  "companyId": "string | null",
  "dealId": "string | null",
  "dueDate": "ISO date string",
  "completed": false
}
```

**Response:** `Activity`

---

### `PUT /api/activities/:id`
Replaces an activity.

**Response:** `Activity`

---

### `PATCH /api/activities/:id`
Partially updates an activity (e.g., toggle `completed`).

**Response:** `Activity`

---

### `DELETE /api/activities/:id`
Deletes an activity.

**Response:** `204 No Content`

---

## Settings

### `GET /api/settings/:userId`
Returns settings for a user.

**Response:** `Settings`

---

### `PUT /api/settings/:userId`
Replaces settings for a user.

**Response:** `Settings`

---

### `PATCH /api/settings/:userId`
Partially updates settings.

**Response:** `Settings`

---

## Dashboard

### `GET /api/dashboard`
Returns aggregated stats for the dashboard.

**Response:**
```json
{
  "totalContacts": 0,
  "totalCompanies": 0,
  "totalDeals": 0,
  "totalActivities": 0,
  "dealsByStage": {
    "lead": { "count": 0, "value": 0 },
    "qualified": { "count": 0, "value": 0 }
  },
  "winRate": 0,
  "recentDeals": [],
  "upcomingActivities": []
}
```
