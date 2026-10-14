# Ship-Ready AI Rules: free sample (Next.js + Supabase + Stripe)

**Your AI agent will happily write `getSession()` on the server, a table without RLS, or a Stripe webhook that grants access twice, or never.** These rules stop that. Drop two files into your repo and Cursor, Claude Code and Codex follow them.

## Quick start
```bash
curl -O https://raw.githubusercontent.com/edtrackai/ship-ready-ai-rules-free-sample/main/AGENTS.md
mkdir -p .cursor/rules && curl -o .cursor/rules/30-stripe.mdc https://raw.githubusercontent.com/edtrackai/ship-ready-ai-rules-free-sample/main/.cursor/rules/30-stripe.mdc
```
Claude Code users: add `@AGENTS.md` to `CLAUDE.md` (or copy `AGENTS.md` to `CLAUDE.md`).

## What's in this free sample
| File | What it does |
|---|---|
| `AGENTS.md` | Stack notes and the 8 **golden rules**: two Supabase clients, RLS in every migration, `getUser()` not `getSession()`, verified Stripe webhooks with retry-safe idempotency, server-only secrets |
| `.cursor/rules/30-stripe.mdc` | The complete Cursor rule for Stripe Checkout, Billing and webhooks: raw-body signature checks, `pending` → `completed` event tracking so a failed event is retried rather than lost, and multi-item-safe billing periods (Stripe API `2025-03-31.basil`+) |

## The full pack
**[Ship-Ready AI Rules v2](https://luxurydrive0.gumroad.com/l/ffjsf?utm_source=github&utm_medium=readme&utm_campaign=ship-ready-ai-rules-free-sample)** adds:
- **Guardrail hooks** for Claude Code that block `.env` reads, remote migrations, Stripe live mode and prod deploys, and fail closed if the guard breaks
- **18 skills and 6 subagents** (RLS migrations and audit, server auth, Stripe Checkout, webhooks and subscriptions, tests, pre-merge audit)
- All 6 Cursor rules, a Claude Code plugin, and one `AGENTS.md` synced to Codex, Gemini CLI, Copilot, Windsurf and Cline
- A tested Next.js 16 + Supabase + Stripe reference app, the pre-launch security checklist and a prompt library

More details: https://edtrackai.github.io/ai-rules?utm_source=cursor-directory&utm_medium=directory&utm_campaign=ai-rules-discovery-1014

## Before you launch
- **Free CLI:** [nextjs-supabase-stripe-security-checker](https://github.com/edtrackai/nextjs-supabase-stripe-security-checker) runs 22 static checks locally in one command.
- **[Launch Audit](https://luxurydrive0.gumroad.com/l/launch-audit?utm_source=github&utm_medium=readme&utm_campaign=ship-ready-ai-rules-free-sample):** a pre-launch security audit with a ready / not-ready report and fix plan.
- **[Ship It Bundle](https://luxurydrive0.gumroad.com/l/ship-it-bundle?utm_source=github&utm_medium=readme&utm_campaign=ship-ready-ai-rules-free-sample):** AI Rules v2 + Launch Audit + Solo Founder OS Pro.
- **[Paid MCP Starter](https://luxurydrive0.gumroad.com/l/paid-mcp-starter?utm_source=github&utm_medium=readme&utm_campaign=ship-ready-ai-rules-free-sample):** charge for your MCP server with Next.js + Supabase + Stripe.
- Free [security checklist](https://luxurydrive0.gumroad.com/l/security-checklist?utm_source=github&utm_medium=readme&utm_campaign=ship-ready-ai-rules-free-sample).

Read more: [7 security bugs AI agents write in Next.js + Supabase + Stripe apps](https://dev.to/edtrackai/7-security-bugs-ai-agents-write-in-nextjs-supabase-stripe-apps-and-the-rules-that-stop-them-3o64)

## License
MIT. See `LICENSE`.
