# Stockroom - React frontend for the LavaLust Product API

React 18 + Vite + Axios. Features: login / register, product list (with search),
add, edit, delete, logout. Token refresh is automatic. The app talks **only** to the LavaLust API
(never directly to Aiven MySQL).

## Run

```bash
npm install
cp .env.example .env     # set VITE_API_URL (API base URL, no trailing slash)
npm run dev              # http://localhost:5173
```
The API must allow this origin: set `CORS_ORIGIN=http://localhost:5173` in the API `.env`.

## Deploy (Render)

The included `render.yaml` configures this repository as a Render Static Site. In Render, create a Blueprint from the frontend repository, then set `VITE_API_URL` to the deployed backend URL (no trailing slash). The static site builds with `npm ci && npm run build` and publishes `dist`.

Deploy the API first using the backend repository's `render.yaml` and Dockerfile. Add the database and token secrets in the backend service's Render environment; do not commit `.env` files or production secrets. After the frontend has a URL, set the backend's `CORS_ORIGIN` to that exact URL and redeploy the backend.

For manual setup, create a Render Static Site with root directory `.`, build command `npm ci && npm run build`, publish directory `dist`, and environment variable `VITE_API_URL=https://<your-api>.onrender.com`.
