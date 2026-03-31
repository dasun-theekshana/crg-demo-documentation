# Sitemap Metadata

The `crm-sitemap.json` file provides CRG with a structured description of the application to bootstrap its understanding without requiring a full probe training run.

## Why a Sitemap?

RDF triples (which CRG uses internally) can capture individual facts but struggle to represent:

- Page hierarchy and parent-child navigation structure
- Route paths and URL patterns
- Role-based access control context
- Interactive element effects and side effects
- Data flow dependencies between pages

The sitemap fills these gaps with structured metadata.

## Sitemap Categories

### 1. Page Registry

Metadata about each page:

```json
{
  "id": "contacts",
  "route": "/contacts",
  "title": "Contacts",
  "description": "Manage person contacts including leads, customers, and prospects",
  "category": "crm-data",
  "discoveredAt": "2025-01-01T00:00:00Z"
}
```

### 2. Navigation Hierarchy

Parent-child relationships derived from the sidebar navigation:

```json
{
  "parent": "app-root",
  "children": ["dashboard", "contacts", "companies", "deals", "activities", "settings"]
}
```

### 3. Sections & UI Regions

Named logical regions within pages (e.g., stats cards, data table, modals).

### 4. Interactive Elements & Actions

Buttons, forms, and links with their effects:

```json
{
  "element": "Create Contact button",
  "action": "opens ContactModal",
  "effect": "POST /api/contacts, refreshes contact list"
}
```

### 5. Data Flows & Dependencies

How data moves between pages and which API endpoints each page depends on.

### 6. Accessibility & Role-Based Access

Permission context — which roles can access which features.

## Files

| File | Description |
|------|-------------|
| `crm-sitemap.json` | Machine-readable sitemap consumed by CRG |
| `crm-sitemap.md` | Human-readable version of the same sitemap |
| `SITEMAP_METADATA_DESIGN.md` | Design document explaining the sitemap architecture |
