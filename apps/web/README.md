# Clip Lab Browser UI

This is the optional React/Vite browser surface for Clip Lab. It is intentionally secondary to the
backend pipeline, CLI, API, renderer service, and Docker workflow.

Use it when you want a lightweight local interface for creating jobs, polling status, and inspecting
completed clips. It is not an account system, hosted dashboard, or production web product.

## Local Development

```bash
npm ci
npm run lint
npm run build
npm run dev
```

The UI expects the FastAPI service to be reachable at `VITE_API_BASE_URL` or
`http://localhost:8000` by default.

## Docker

The browser UI is behind the `web` Compose profile:

```bash
docker compose --profile web up --build
```
