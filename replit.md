# Thenmozhi Designs

A premium Indian fashion storefront for discovering handloom sarees, salwar suits, kurtas, dresses, and blouses from a Chennai atelier.

## Run & Operate

- `pnpm --filter @workspace/api-server run dev` — run the API server (port 5000)
- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from the OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- Required env: `DATABASE_URL` — Postgres connection string

## Stack

- pnpm workspaces, Node.js 24, TypeScript 5.9
- API: Express 5
- DB: PostgreSQL + Drizzle ORM
- Validation: Zod (`zod/v4`), `drizzle-zod`
- API codegen: Orval (from OpenAPI spec)
- Build: esbuild (CJS bundle)

## Where things live

- `artifacts/thenmozhi-designs/src/App.tsx` — storefront routes, structured catalog, local shopping state, cart, wishlist, checkout, and product interactions
- `artifacts/thenmozhi-designs/src/index.css` — Thenmozhi Designs visual language and responsive styling
- `attached_assets/` — supplied reference screenshots and product/editorial imagery
- `artifacts/api-server/` — shared Express API service (currently only the starter health route)

## Architecture decisions

- The first storefront build is frontend-first and uses structured TypeScript catalog data with localStorage for guest cart and wishlist persistence.
- Product, customization, gift-wrap, discount, shipping, and checkout totals are kept in one local commerce flow so selections persist from product detail through confirmation.
- The uploaded screenshot assets are used as the visual source material; hero cropping intentionally removes embedded source-site chrome before display.
- Live payment and fulfillment are not enabled until a commerce provider is connected; the checkout currently completes as an explicit local order state.

## Product

Users can browse the home page and collections, search and filter the catalog, inspect products with galleries and accordions, save wishlist items, add size/customization/gift-wrap choices to a persistent cart, apply a discount, validate checkout details, and reach an order confirmation state.

## User preferences

_Populate as you build — explicit user instructions worth remembering across sessions._

## Gotchas

- The app is registered at the root preview path and runs through the managed `artifacts/thenmozhi-designs: web` workflow.
- If live checkout is added later, replace the local checkout completion with a connected commerce provider and move price, stock, tax, shipping, and order validation server-side.

## Pointers

- See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details
