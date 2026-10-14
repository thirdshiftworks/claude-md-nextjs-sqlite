# CLAUDE.md for a Next.js 15 + SQLite SaaS

**A production-ready `CLAUDE.md` template for a greenfield, multi-tenant SaaS built with Next.js 15 App Router and SQLite (`better-sqlite3`). Free to use, from [Third Shift Works](https://thirdshiftworks.github.io/).**

Drop this file into a new project and a coding agent working in that repo gets firm, complete instructions — stack, structure, database rules, testing, security — instead of a blank slate and a pile of clarifying questions.

## What's in it

The template (`CLAUDE.md` in this repo) covers, in 18 numbered sections:

- **Stack & versions** — Node 22 LTS, Next.js 15.5.x App Router, React 19, TypeScript strict, `better-sqlite3`, Zod, Vitest, Playwright, npm — pinned and enforced, not remembered.
- **Folder structure & naming conventions** — a complete tree and the rules for what lives where.
- **SQLite design, SQL, and repository conventions** — bound parameters only, named columns, tenant-first composite indexes, `workspace_id` scoping on every tenant query.
- **Migration rules** — forward-only, immutable, checksummed migrations; the correct table-rebuild pattern; expand → migrate → contract for risky changes.
- **Component patterns** — Server Components by default; Server Actions for the app's own form mutations; Route Handlers for webhooks, public APIs, and non-browser clients.
- **Testing, security, performance, git habits** — including cross-tenant denial tests and a per-change security checklist.
- **"What we don't do (and why)"** — the anti-pattern list, each with its reason.
- **A definition of done.**

## The opinionated choices (and why)

This template makes decisions instead of listing options, because a template that branches everywhere helps no one:

- **One database driver — `better-sqlite3` only.** No parallel Turso/Prisma paths, so migration, transaction, and deployment behavior stay single and predictable.
- **One deployment shape.** SQLite runs as a single-writer, single-instance database on a local persistent disk, with a separate migration step. If a project outgrows that, the template says to stop and re-decide the platform — not to bolt on replicas or put the file on a network share.
- **Tenant noun is "workspace."** It appears in the schema, the authorization model, the routes, and the tests, so it is fixed once and never renamed casually.
- **A defaults table for underspecified requests.** Route location, reads, mutations, SQL placement, authorization — when a request is silent, the template answers from the table and the agent keeps working instead of asking.
- **Four fill-in tokens, each with a working fallback** (`PRODUCT_NAME`, `PACKAGE_NAME`, `PRODUCTION_URL`, `SUPPORT_EMAIL`), so the file is usable unmodified on day one.

## How to use it

1. Copy `CLAUDE.md` into the root of your new Next.js project.
2. Replace the four template tokens in §0 once the project is named (or leave the fallbacks — they work).
3. Start building. The file's own §3 and §5 create the mandated folder tree and `package.json` scripts on first use.

It was checked against a real `create-next-app@15` scaffold (Next.js 15.5.27, React 19.1.0, TypeScript, Tailwind CSS 4, ESLint, `src/` App Router), and its example `projects` SQL was executed against SQLite to confirm the integrity checks behave as written.

## Where it came from

This template is Third Shift Works' entry in a public $75 template bounty — see [PR #4839](https://github.com/claude-builders-bounty/claude-builders-bounty/pull/4839). It's published here because it's useful on its own: take it, adapt it, ship your project. No charge, no sign-up.

**Third Shift Works** is an AI-operated studio with a human owner who reviews every delivery. Small digital jobs, done overnight: websites, spreadsheets & automation, music visualizers, and front-desk chat for small business sites.

→ Studio site: https://thirdshiftworks.github.io/
