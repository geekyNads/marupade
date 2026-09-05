# ಮರುಪಡೆ (Marupaḍe) — Intelligent Lost & Found Recovery

Marupaḍe ("to reclaim/get back" in Kannada) is a trust-driven lost & found platform concept for a campus community. It pairs a smart matching engine with reputation, verification, and fraud-detection mechanics so recovered items reliably get back to their rightful owners — not just whoever asks first.

## Features

- **Browse & report** — Post lost or found items with category, location, condition, urgency, and reward fields, plus sealed *hidden attributes* that are never shown publicly and are used only to verify a claimant.
- **Smart search** — A Trie-based prefix index combined with Levenshtein-distance fuzzy matching and Jaccard token-similarity scoring, so search tolerates typos and partial descriptions.
- **Guardian Assistant** — A conversational interface where a user describes what they lost in plain language and gets back likely matches and probable locations.
- **Ownership verification** — Claimants answer weighted verification questions derived from an item's hidden attributes before a match is confirmed.
- **Reputation & leaderboard** — Trust scores, karma, ranks (New Member → Legend), badges, and a campus-wide Hall of Fame that rewards honest returns.
- **Admin control center** — Review claims, ownership-confidence scores, and fraud-risk signals for items and users.
- **Campus analytics** — Recovery rates, loss heatmaps by building, peak-loss hours, and monthly trend charts.

## Tech stack

- [TanStack Start](https://tanstack.com/start) (React 19) with file-based routing via TanStack Router
- [Nitro](https://nitro.build/) as the server/deploy toolkit (SSR, server functions, deploy-anywhere output)
- [TanStack Query](https://tanstack.com/query) for data/state
- Tailwind CSS v4 + [shadcn/ui](https://ui.shadcn.com/) (Radix UI primitives) for the component library
- Recharts for analytics visualizations
- TypeScript throughout

## Getting started

```bash
# install dependencies
npm install   # or: bun install

# start the dev server
npm run dev

# type-check / lint
npm run lint

# production build
npm run build

# preview the production build locally
npm run preview
```

The dev server runs at `http://localhost:3000` by default.

## Project structure

```
src/
├── routes/                 # File-based routes (TanStack Router)
│   ├── index.tsx           # Landing page
│   ├── browse.tsx          # Search & filter items
│   ├── report.tsx          # Report a lost/found item
│   ├── items.$id.tsx       # Item detail + claim/verification flow
│   ├── assistant.tsx       # Guardian Assistant chat
│   ├── leaderboard.tsx     # Reputation & Hall of Fame
│   ├── analytics.tsx       # Campus-wide recovery analytics
│   ├── admin.tsx           # Admin control center
│   └── sitemap[.]xml.ts    # Sitemap route
├── components/
│   ├── guardian/           # App-specific components (AppShell, ItemCard, widgets)
│   └── ui/                 # shadcn/ui component library
├── lib/
│   └── guardian/
│       ├── types.ts        # Domain types (Item, User, Rank, etc.)
│       ├── data.ts         # Mock/sample data
│       └── engine.ts       # Search, matching, scoring, and ranking logic
├── router.tsx               # Router + QueryClient setup
├── start.ts                  # TanStack Start server config & error middleware
└── server.ts                 # Server entry with error-page fallback
```

## Deployment

This app deploys to any Nitro-supported target (Vercel, Netlify, Cloudflare, Node, Bun, etc.). The Vite config includes the Nitro plugin (`nitro/vite`), which compiles the server output for the target platform — on Vercel this is auto-detected with zero extra configuration, producing Vercel Functions for SSR and server routes.

```bash
npm run build   # outputs to .output/
```
