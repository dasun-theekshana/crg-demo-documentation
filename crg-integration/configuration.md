# CRG Configuration

CRG is configured via environment variables in `crm/.env`.

## Environment Variables

| Variable | Required | Description |
|----------|----------|-------------|
| `VITE_CRG_ENABLED` | Yes | Set to `true` to enable CRG, `false` to disable |
| `VITE_CRG_APP_ID` | Yes | Unique identifier for this host application |
| `VITE_CRG_SERVICE_URL` | Yes | URL of the CRG core service |
| `VITE_CRG_GRAPH_SERVICE_URL` | Yes | URL of the CRG graph/probe service |
| `VITE_CRG_SOURCE_CODE_PATH` | No | Absolute path to source code for probe analysis |

## Example `.env`

```env
VITE_CRG_ENABLED=true
VITE_CRG_APP_ID=crm-demo
VITE_CRG_SERVICE_URL=http://localhost:3001
VITE_CRG_GRAPH_SERVICE_URL=http://localhost:8002
VITE_CRG_SOURCE_CODE_PATH=C:\Altrium\concierge\people-os-src
```

## Runtime Configuration Object

In `main.tsx`, environment variables are composed into the CRG config object:

```ts
const crgConfig = {
  appId: import.meta.env.VITE_CRG_APP_ID,
  serviceUrl: import.meta.env.VITE_CRG_SERVICE_URL,
  graphServiceUrl: import.meta.env.VITE_CRG_GRAPH_SERVICE_URL,
  sourceCodePath: import.meta.env.VITE_CRG_SOURCE_CODE_PATH,
  userRole: 'admin',
  userId: 'demo-user-001',
  backgroundCapture: {
    enabled: true,
    debounceMs: 1000,
    trackMutations: true,
    hashContent: true,
    mutationThreshold: 10,
  },
}
```

## User Context

The `userRole` and `userId` fields are hardcoded to `'admin'` and `'demo-user-001'` in the demo. In a production integration these would be sourced from your authentication system.

## Disabling CRG

Set `VITE_CRG_ENABLED=false` to run the CRM without any CRG integration. The app renders and functions identically — no CRG components are mounted and no CRG packages are initialized.
