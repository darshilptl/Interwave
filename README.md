# Interwave

> The open-source Intercom. Built for developers. Free to self-host.

Intercom priced out the developers who needed it most. Interwave gives it back.

Self-hostable customer support infrastructure — Linear-style UI, MCP and SDK native from day one, AI that knows your product, and a free tier that is actually free. No upgrade walls. No vendor lock-in. No invoice surprises.

---

## Why this exists

Intercom is good software. It is also software that has systematically priced out the people who build software.

No real free tier. AI locked behind a premium add-on. No MCP tools. No self-hosting. A UI that was designed for support agents, not for developers who want to move fast. And if you want your own model — you cannot. You take theirs, at their price, on their terms.

Interwave is the alternative that should have existed already.

Open source core. Genuine free tier. MCP and SDK built in — not bolted on later. AI that is trained on your product, not a generic bot. A UI that thinks like Linear. Deployable in one command. Your data, your infrastructure, your call.

---

## What is open source

The entire core platform is MIT licensed and free to self-host.

- **Dashboard** — full support inbox, conversation management, team assignment
- **Widget** — embeddable chat widget for your product or website
- **Contacts** — full contact management with conversation history
- **Webhooks** — event system for conversation lifecycle
- **Docs site** — documentation and integration guides
- **REST API** — complete API surface for contacts, conversations, workspace, webhooks

```
Interwave/
├── apps/
│   ├── web/          ← Main dashboard (Next.js 15)
│   ├── widget/       ← Embeddable chat widget
│   └── docs/         ← Documentation site
├── packages/
│   ├── db/           ← Drizzle client, schema, migrations (Supabase + Postgres)
│   ├── auth/         ← BetterAuth config, shared across apps
│   ├── ui/           ← Shared component library, design tokens
│   └── validators/   ← All Zod schemas, shared validation
```

## What is not open source

Premium features are built and maintained in a private repository. They are available on the paid tier.

- **AI agents** — trained on your product, scoped to support conversations
- **MCP tools** — Model Context Protocol integration and SDK
- **Outbound campaigns** — proactive messaging engine
- **Advanced analytics** — conversation metrics, team performance
- **Priority support** — direct access, SLA guarantees

Payments are handled via **Polar.sh** for open source sponsorship and **Dodo Payments** for premium subscriptions.

The open source core will never be crippled to push you toward paid. That is the promise.

---

## How it is built

Every decision in this stack was made for one reason — to keep self-hosting simple and performance uncompromised.

| Layer | Choice | Why |
|---|---|---|
| Framework | Next.js 15 | App router, server components, single deployment unit |
| ORM | Drizzle | Zero runtime overhead, raw SQL performance, full TypeScript types from schema |
| Database | Supabase (Postgres) | Managed Postgres, real-time subscriptions, storage — Drizzle connects directly |
| Auth | BetterAuth | Framework-agnostic, shared across all apps via `packages/auth` |
| Validation | Zod | Single schema definition, shared between client and server via `packages/validators` |
| State | Zustand | Minimal, no boilerplate, scoped to UI state only |
| Monorepo | Turborepo | Shared packages across dashboard, widget, and docs without duplication |
| Monitoring | Sentry | Error tracking across all apps from day one, not added later |
| CI/CD | GitHub Actions | Lint, typecheck, build on every PR — nothing ships broken |
| Payments | Polar.sh + Dodo Payments | Open source sponsorship and premium billing, kept separate by intent |

**On Drizzle specifically** — Drizzle connects directly to your Supabase Postgres connection string. No binary. No adapter layer. No cold start penalty. Migrations are plain SQL files you can read and version. If you have used Prisma, Drizzle will feel faster and more honest.

---

## API surface

```
── Conversations
   GET     /conversations
   POST    /conversations
   GET     /conversations/:id
   PATCH   /conversations/:id
   POST    /conversations/:id/messages
   PATCH   /conversations/:id/assign
   PATCH   /conversations/:id/status

── Contacts
   GET     /contacts
   POST    /contacts
   GET     /contacts/:id
   PATCH   /contacts/:id
   DELETE  /contacts/:id
   GET     /contacts/:id/conversations

── Widget
   POST    /widget/identify
   POST    /widget/conversations
   POST    /widget/conversations/:id/messages

── Webhooks
   GET     /webhooks
   POST    /webhooks
   GET     /webhooks/:id
   DELETE  /webhooks/:id
   POST    /webhooks/:id/test

── Workspace
   GET     /workspace
   GET     /workspace/agents

── Events (payloads sent to your webhook URLs)
   conversation.created
   conversation.assigned
   conversation.resolved
   message.created
   contact.created
```

---

## Getting started

> **Current status:** Architecture complete. Turborepo workspace configured. Design tokens in progress. Auth, dashboard, and core features integrating actively.
>
> The foundation is being built with the same care as the spec. Self-host instructions will be here the moment the first working version is ready.

```bash
# Clone the repo
git clone https://github.com/darshilptl/Interwave.git
cd Interwave

# Install dependencies
pnpm install

# Set up environment variables
cp .env.example .env.local
# Add your Supabase connection string and BetterAuth secret

# Run the dashboard locally
pnpm dev
```

Full self-host documentation — including Docker setup and one-command deployment — will live at `docs.Interwave.dev` once the core ships.

---

## Building principles

These are not opinions. They are the constraints every decision is checked against.

**Every phase ships something a real user can use.**
No phase ends with "infrastructure work." Each one delivers a thing a real person can open and use.

**AI and MCP are not phase 3 afterthoughts. They are phase 2.**
The architecture was designed around them from day one. They are not integrations. They are load-bearing.

**The open source core will never be a crippled version of the paid product.**
The core is complete support infrastructure. Premium is additional capability — not features held back to force an upgrade.

**Design is not polish. Design is phase 1.**
The UI is built on a Linear-style design system defined before the first component. Consistency is not an afterthought.

---

## Contributing

Interwave is in active foundation development. The contributing window is not fully open yet — and this README will not pretend otherwise.

**What is welcome right now:**

If you see a UI component, layout, or interaction pattern that is clearly better than what exists and aligns with the Linear-style design system — open a PR. Design improvements with clear reasoning are welcome before the auth layer ships.

**What is not ready yet:**

Feature contributions, integrations, and core logic changes are not open for PRs until the auth layer is implemented and stable. Contributing to moving parts causes more problems than it solves.

**When the first contribution window opens:**

The first PR-ready milestone is auth implementation. Once that ships, the contributing guide will update with specific areas, good first issues, and what kind of contributions have the most impact.

Until then — **star the repo and watch**. You will know exactly when it is ready.

For questions, architecture discussions, or if you want to follow the build: [@darshilptl](https://twitter.com/darshilptl)

---

## License

MIT — see [LICENSE](./LICENSE)

The core is free. The trust is the foundation. The business is built on top of both.

---

*Built by [Darshil Patel](https://darshilptl.com)*
