# Ship-Ready AI Rules: free sample (Next.js + Supabase + Stripe)

**Your AI agent will happily write `getSession()` on the server, a table without RLS, or a Stripe webhook that grants access twice, or never.** These rules are written to steer it away from that. Drop two files into your repo and Cursor, Claude Code and Codex follow them.

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

## Install as a Cursor plugin
This repo is also a Cursor plugin (`.cursor-plugin/plugin.json`). It contains the one free rule, `.cursor/rules/30-stripe.mdc`. There are no hooks, agents, skills or MCP servers in it. The plugin is validated against Cursor's documented plugin format with Cursor's own validator script and schemas (from the `cursor/plugins` repository); it has not been tested in a live Cursor session.

**Local install**
```bash
git clone https://github.com/edtrackai/ship-ready-ai-rules-free-sample ~/.cursor/plugins/local/ship-ready-ai-rules-free-sample
```
Then restart Cursor or run **Developer: Reload Window**, and open **Customize** to check that the rule is listed. On Teams and Enterprise plans, an admin may need to turn on **Allow Local Plugin Imports**. The plugin doesn't include `AGENTS.md`; copy it into your repo root as in the quick start if you want the golden rules too.

**Team marketplace (Teams and Enterprise plans)**
An admin opens **Dashboard → Plugins & MCPs → Team Marketplaces → Add Marketplace → Import from Repo** and pastes `https://github.com/edtrackai/ship-ready-ai-rules-free-sample`. The repo's `.cursor-plugin/marketplace.json` lists the plugin.

Don't use the plugin and a copied `.cursor/rules/30-stripe.mdc` in the same project, or the rule appears twice.

## The full pack
Ad (our own paid product): Ship-Ready AI Rules v2, $19 (plus VAT where applicable): https://luxurydrive0.gumroad.com/l/ffjsf?utm_source=github&utm_medium=readme&utm_campaign=cursor-plugin&utm_content=ship-ready-ai-rules-free-sample

Everything in this repo stays free. AI Rules v2 adds:
- **Guardrail hooks** for Claude Code designed to refuse `.env` reads, remote migrations, Stripe live mode and prod deploys, and to fail closed if the guard itself errors
- **18 skills and 6 subagents** (RLS migrations and audit, server auth, Stripe Checkout, webhooks and subscriptions, tests, pre-merge audit)
- All 6 Cursor rules, a Claude Code plugin, and one `AGENTS.md` synced to Codex, Gemini CLI, Copilot, Windsurf and Cline
- A tested Next.js 16 + Supabase + Stripe reference app, the pre-launch security checklist and a prompt library

More details: https://edtrackai.github.io/ai-rules?utm_source=cursor-directory&utm_medium=directory&utm_campaign=ai-rules-discovery-1014

## Before you launch
- **Free CLI:** [nextjs-supabase-stripe-security-checker](https://github.com/edtrackai/nextjs-supabase-stripe-security-checker) runs 24 static checks locally in one command.
- *Ad (paid, same author):* **[Launch Audit](https://luxurydrive0.gumroad.com/l/launch-audit?utm_source=github&utm_medium=readme&utm_campaign=ship-ready-ai-rules-free-sample):** a pre-launch security audit with a ready / not-ready report and fix plan.
- **[Ship It Bundle](https://luxurydrive0.gumroad.com/l/ship-it-bundle?utm_source=github&utm_medium=readme&utm_campaign=ship-ready-ai-rules-free-sample):** AI Rules v2 + Launch Audit + Solo Founder OS Pro.
- **[Paid MCP Starter](https://luxurydrive0.gumroad.com/l/paid-mcp-starter?utm_source=github&utm_medium=readme&utm_campaign=ship-ready-ai-rules-free-sample):** charge for your MCP server with Next.js + Supabase + Stripe.
- Free [security checklist](https://luxurydrive0.gumroad.com/l/security-checklist?utm_source=github&utm_medium=readme&utm_campaign=ship-ready-ai-rules-free-sample).

Read more: [7 security bugs AI agents write in Next.js + Supabase + Stripe apps](https://dev.to/edtrackai/7-security-bugs-ai-agents-write-in-nextjs-supabase-stripe-apps-and-the-rules-that-stop-them-3o64)

## Related free tools

- [Next.js Supabase Stripe Security Checker](https://github.com/edtrackai/nextjs-supabase-stripe-security-checker): free CLI and GitHub Action, 24 static checks for keys, auth, RLS and Stripe webhooks.
- [ship-ready-skills](https://github.com/edtrackai/ship-ready-skills): free Agent Skills that review Supabase RLS and grants, and Stripe webhook handlers (`npx skills add edtrackai/ship-ready-skills`).

## License
MIT. See `LICENSE`.

Cursor is a trademark of Anysphere, Inc. Claude and Claude Code are trademarks of Anthropic. Codex, Next.js, Supabase and Stripe are trademarks of their respective owners. This project is not affiliated with or endorsed by any of them.
