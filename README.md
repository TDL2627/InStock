# InStock

InStock is an inventory tracker and point-of-sale (POS) app for small shops, built with Next.js and Supabase. It focuses on simple workflows for a single owner and one or more tellers: add and manage products, record sales (orders), and view basic sales reports.

Author: TDL2627

The app in this repository includes:
- Next.js frontend (React) under `src/`
- Supabase integration (auth + database) via `src/lib/supabaseClient.js`
- Simple client-side stores and utilities for products, orders and auth

## Quick start

Prerequisites
- Node.js 18+ and npm/yarn/pnpm
- A Supabase project (for database and auth)

1) Install dependencies

```bash
npm install
```

2) Create environment variables

Create a `.env.local` in the repository root with these values (replace with your Supabase values):

```
NEXT_PUBLIC_SUPABASE_URL=https://your-project.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=public-anon-key
```

3) Import sample data (optional)

You can import CSV templates included in `supabase_csv/` into your Supabase tables (Table editor → Import). See the `supabase_csv/` directory in this repo for `users.csv`, `products.csv`, and `orders.csv`.

4) Run the dev server

```bash
npm run dev
```

Open http://localhost:3000 in your browser.

## Build & production

To build for production:

```bash
npm run build
npm start
```

Or deploy to Vercel. The app is a standard Next.js app and works with Vercel out of the box. Make sure to add the Supabase env vars in Vercel's project settings.

## Project structure (important files)

- `src/pages/` - Next.js pages (auth, dashboard, products, sales, tellers)
- `src/app/` - app-level components, global styles
- `src/lib/supabaseClient.js` - Supabase client initialization
- `src/utils/*` - helper functions for auth, products and orders
- `supabase_csv/` - sample CSVs for quick import into Supabase

## Supabase CSV templates

CSV templates for quick import into Supabase (Table editor → Import):

users.csv

```text
id,email,name,role,ownerEmail
00000000-0000-0000-0000-000000000000,owner@example.com,Alice Owner,owner,
11111111-1111-1111-1111-111111111111,teller@example.com,Bob Teller,teller,owner@example.com
```

products.csv

```text
id,name,category,price,quantity,image_url,ownerEmail
1,Cola,Drinks,12.50,24,https://example.com/cola.png,owner@example.com
2,Bread,Food,18.00,10,https://example.com/bread.png,owner@example.com
```

orders.csv

```text
id,orderDate,totalAmount,cardFee,paymentMethod,items,teller,ownerEmail
aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa,2025-01-01T10:00:00Z,30.50,0.00,cash,"[{""productId"":1,""name"":""Cola"",""price"":12.5,""quantity"":2}]",Bob Teller,owner@example.com
bbbbbbbb-bbbb-bbbb-bbbb-bbbbbbbbbbbb,2025-01-02T12:00:00Z,120.00,5.00,card,"[{""productId"":2,""name"":""Bread"",""price"":18,""quantity"":4}]",Bob Teller,owner@example.com
```

Notes
- The `items` column in `orders.csv` stores JSON as a string inside the CSV — use a CSV importer that preserves JSON quotes properly (or import programmatically).

## Development notes & tips

- If auth isn't working, confirm your Supabase URL and anon key are correct and that CORS settings in Supabase allow your dev origin.
- The app assumes an `owner` user and `teller` roles. Use the `users.csv` sample to seed initial users.

## Contributing

Bug reports and pull requests are welcome. For larger changes, open an issue first so we can discuss design.

## License

This project is provided as-is. Add a LICENSE file if you want an explicit license.
