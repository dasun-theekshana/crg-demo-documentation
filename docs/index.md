# CRG Demo CRM

A demonstration **Customer Relationship Management (CRM)** application built as a host application for the **CRG (Conversational Product Intelligence)** platform.

## What is this project?

This monorepo contains a full-stack CRM application designed to showcase CRG's ability to understand, navigate, and assist users within a real-world web application through conversational intelligence.

The app provides a realistic CRM experience covering contacts, companies, deals, and activities — while being fully instrumented with the CRG connector for probe training and conversational assistance.

## Project Structure

```
crg-demo-host-app-crm/
├── crm/          # React frontend (Vite + TailwindCSS)
├── crm-api/      # Hono backend (Cloudflare Workers compatible)
├── docs/         # This documentation
└── mkdocs.yml    # Documentation configuration
```

## Quick Start

```bash
npm install
npm run dev
```

- **Frontend:** http://localhost:5173
- **API:** http://localhost:8787

## Key Features

| Feature | Description |
|---------|-------------|
| Dashboard | Metrics overview, pipeline summary, recent deals |
| Contacts | Create, search, and manage person contacts |
| Companies | Manage organizations with parent-child hierarchy |
| Deals | Track sales pipeline with stage-based workflow |
| Activities | Log calls, emails, meetings, tasks, and notes |
| Settings | User preferences for theme, notifications, currency |

## Tech Stack

| Layer | Technology |
|-------|------------|
| Frontend | React 19, Vite, TailwindCSS 4, TypeScript |
| Routing | React Router v7 |
| Icons | Lucide React |
| Backend | Hono 4, Node.js dev / Cloudflare Workers prod |
| Testing | Vitest |
| CRG | @crg/connector-react, @crg/connector-core, @crg/sidecar-ui |
