# Team Task Manager

## Overview
This monorepo contains a **frontend** built with React + Vite and a **backend** built with Express and TypeScript. The project is configured as a Yarn/NPM workspace, allowing shared libraries under `lib/`.

## Features
- User authentication (JWT, bcrypt)
- CRUD operations for projects, tasks and users
- Rate limiting, security headers, and CORS configuration
- Centralised logging with `pino`
- Shared TypeScript types via `api-zod`
- Database integration with MongoDB (via `@workspace/db`)

## Architecture Flow
```mermaid
graph LR
    A[Client (Browser)] -->|HTTP| B[Express Server]
    B -->|API Calls| C[MongoDB]
    B -->|Static Files| D[Built Frontend (dist/public)]
    D -->|Served to| A
```

## Development
Run the entire application with a single command from the repository root:

```bash
npm run dev
```

This uses `concurrently` to start both the frontend dev server (Vite) and the backend server (tsx). The frontend proxies API requests to the backend via the Vite proxy configuration.

## Production
To build and start the app on a single port (default `PORT` env variable):

```bash
npm run start
```

The `start` script builds the frontend, builds the backend, and then runs the compiled backend which serves the static frontend files.

## Railway Deployment
The repository includes a `Procfile` for Railway (or any Heroku‑compatible platform):

```
web: npm run start
```

Railway will set the `PORT` environment variable automatically. Ensure the environment variables required by the backend (`MONGODB_URI`, `JWT_SECRET`, etc.) are added in the Railway dashboard.

## Scripts
| Script | Description |
|--------|-------------|
| `npm run dev` | Starts both frontend and backend in development mode |
| `npm run build` | Type‑checks and builds all workspace packages |
| `npm run start` | Builds the project and starts the production server |

## License
MIT
