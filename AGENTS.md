# AGENTS.md: Next.js + Supabase + Stripe

Instructions for AI coding agents (Cursor, Claude Code, Codex, etc.) working in this repo.

## Stack
- Next.js 16 App Router, React 19, TypeScript strict. `proxy.ts` replaces `middleware.ts`.
- Supabase (Postgres + Auth) via `@supabase/ssr` for user sessions and `@supabase/supabase-js` for admin.
- Stripe Checkout + Billing, with subscription state mirrored into Postgres by webhooks.
- Zod for env and input validation.

## Commands
- `npm run dev`: local dev
- `npm run typecheck`: must pass before you finish
- `npm test`: unit tests (tsx + node:test)
- `npm run build`: must pass before you finish
- `stripe listen --forward-to localhost:3000/api/webhooks/stripe`: local webhooks
- `supabase migration new <name>` / `supabase db push`: schema changes

## Golden rules (never break these)
1. **Two Supabase clients, never mixed.** `createUserClient()` (publishable key, RLS applies) for anything acting as a user. `createAdminClient()` (secret key, bypasses RLS) **only** in webhooks, cron jobs and trusted server jobs. Never import the admin client into a Server Component that renders user-controlled data, and never into client code.
2. **Every new table gets RLS enabled in the same migration**, with explicit policies. No policy means no access. That's the correct default for server-only tables.
3. **Auth check = `supabase.auth.getUser()`** on the server. Never trust `getSession()` or client-sent user ids for authorisation.
4. **Stripe webhooks:** read the raw body with `request.text()`, verify with `stripe.webhooks.constructEvent`, record `event.id` as pending and mark it completed only after processing succeeds (reprocess pending retries, 5xx on failure), and return 2xx quickly. Never parse JSON before verifying.
5. **Stripe is the source of truth for billing.** Grant access from the mirrored `subscriptions` row written by webhooks, never from the checkout success redirect.
6. **Secrets live only on the server:** `SUPABASE_SECRET_KEY`, `STRIPE_SECRET_KEY`, `STRIPE_WEBHOOK_SECRET`. Only `NEXT_PUBLIC_*` may reach the browser. Files that touch secrets start with `import "server-only"`.
7. **Validate env with Zod lazily** (`env()`), so `next build` works without secrets but runtime fails loudly.
8. **Schema changes only via new migration files.** Never edit an applied migration. Never run destructive SQL without asking.

- Never `@supabase/auth-helpers-nextjs`, never `using (true)` on user data, always `await params`.

## Auth flow
- Magic link: Server Action → `signInWithOtp` with `emailRedirectTo` = `<SITE_URL>/auth/confirm?next=...`.
- `/auth/confirm` handles `token_hash`+`type` (`verifyOtp`) and PKCE `code` (`exchangeCodeForSession`).
- Never redirect to a raw `next` param. Use `safeNext()` (relative paths only).
- Sign out via POST only.

## Conventions
- Server Components by default. Add `"use client"` only for interactivity.
- Mutations go in Server Actions or Route Handlers; validate input with Zod; return typed results.
- `await cookies()` and `await headers()`: these are async in Next 15+.
- Pages that read the user's data: `export const dynamic = "force-dynamic"` or rely on cookies usage.
- Money: store integer minor units (pence/cents) and the currency code. Never floats.
- Keep pure logic (e.g. status → access mapping) in `lib/` and unit-test it.

## Definition of done
typecheck ✔ · tests ✔ · build ✔ · new tables have RLS + policies · no secret in client bundles · webhook handlers idempotent.
