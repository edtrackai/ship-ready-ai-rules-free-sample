# Ship-Ready AI Rules: free sample (Next.js + Supabase + Stripe)

Rules that stop AI coding agents (Cursor, Claude Code, Codex) from shipping insecure Supabase and Stripe code.

This free sample contains:

| File | What it does |
|---|---|
| `AGENTS.md` | Stack notes and the 8 **golden rules** (two Supabase clients, RLS in every migration, `getUser()` not `getSession()`, verified + idempotent Stripe webhooks, server-only secrets) |
| `.cursor/rules/30-stripe.mdc` | The complete Cursor rule for Stripe Checkout, Billing and webhooks |

## Use it
Copy `AGENTS.md` to your repo root and `.cursor/rules/30-stripe.mdc` into `.cursor/rules/`. Claude Code users can symlink or copy `AGENTS.md` to `CLAUDE.md`.

## The full pack
**[Ship-Ready AI Rules ($15)](https://luxurydrive0.gumroad.com/l/ffjsf)** adds:
- 6 Cursor rules (project, Next.js 16, Supabase/RLS, Stripe, security, testing)
- `CLAUDE.md` and 5 Claude Code skills (add a Supabase table, add a Stripe webhook event, add an auth flow, add a protected page, security review)
- Setup docs, a rules-explained guide and a walkthrough
- The reference Next.js 16 + Supabase + Stripe app the rules were written against
- Bonus: pre-launch security checklist and prompt library

👉 https://luxurydrive0.gumroad.com/l/ffjsf

Read more: [7 security bugs AI agents write in Next.js + Supabase + Stripe apps](https://dev.to/edtrackai/7-security-bugs-ai-agents-write-in-nextjs-supabase-stripe-apps-and-the-rules-that-stop-them-3o64)

## License
MIT. See `LICENSE`.
