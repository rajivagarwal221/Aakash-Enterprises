# Aakash Enterprises

A point-of-sale and inventory system for a beverage distributor: ring up sales, track stock, manage customers and their credit, and see daily and monthly revenue at a glance.

## Features

| Page | What it does |
| --- | --- |
| Overview | Today's revenue, drinks sold, monthly revenue and stock remaining |
| POS | Fast checkout for counter and route sales |
| Products & Inventory | Products, prices and stock levels |
| Customers | Customer list and purchase history |
| Credits & Dues | Outstanding balances and repayments |
| Sales History | Every sale, searchable |
| Analytics & Reports | Revenue and product trends |

## Tech stack

- **Frontend:** React + Vite + Tailwind CSS + shadcn/ui, React Query hooks generated from the API spec
- **Backend:** Express 5 on Node.js, request/response validation with Zod
- **Database:** PostgreSQL (Neon) with Drizzle ORM
- **API contract:** OpenAPI spec with Orval code generation
- **Monorepo:** pnpm workspaces, TypeScript project references
- **Hosting:** frontend on Vercel, API on Render (`render.yaml`)

## Getting started

Requires Node.js 20+ and pnpm.

```bash
git clone https://github.com/rajivagarwal221/Aakash-Enterprises.git
cd Aakash-Enterprises
pnpm install
cp .env.example .env          # set DATABASE_URL
pnpm --filter @workspace/db run push        # create tables
pnpm --filter @workspace/api-server run dev # API
pnpm --filter @workspace/aakash-enterprises run dev   # web app, http://localhost:5173
```

## Project structure

```text
artifacts/
  aakash-enterprises/   React web app (pages in src/pages)
  api-server/           Express API (routes: products, customers, sales, analytics)
  mockup-sandbox/       UI component sandbox
lib/
  api-spec/             OpenAPI spec + Orval config
  api-client-react/     Generated React Query hooks
  api-zod/              Generated Zod schemas
  db/                   Drizzle schema and connection
scripts/                Utility scripts
```

## Scripts

| Command | What it does |
| --- | --- |
| `pnpm run build` | Typecheck, then build every package |
| `pnpm run typecheck` | Typecheck the whole workspace |

More detail on the workspace layout is in [`replit.md`](replit.md).

## Deployment

- **API:** Render builds with `pnpm install && pnpm run build` and starts `artifacts/api-server`. Set `DATABASE_URL` in the Render dashboard.
- **Web:** Vercel serves the built app and proxies `/api/*` to the Render service (`vercel.json`).
