# Working guide

This repository owns the Surrey Neurotech public website and its standalone committee applications service.

## Scope

- `apps/neurotech` is the public site at `https://surreyneurotechsociety.org`.
- `apps/neurotech-applications` is a separate recruitment service and Vercel project.
- `packages/admin`, `packages/assistant`, and `packages/ui` are local workspace packages required by the website.
- The website reads published data from the existing shared Convex deployment through `CONVEX_URL`. Do not add a local Convex schema or deploy a second backend as part of ordinary Neurotech work.

## Commands

Use npm and Node.js 22.12 or newer.

| Check | Command |
| --- | --- |
| Website development | `npm run dev:neurotech` |
| Applications development | `npm run dev:neurotech-applications` |
| TypeScript | `npm run typecheck` |
| Unit tests | `npm test` |
| Website build | `npm run build:neurotech` |
| Applications build | `npm run build:neurotech-applications` |
| Website browser checks | `npm run e2e:site` |
| Applications browser checks | `npm run e2e:applications` |

Run affected checks after changes. Run both builds for shared package changes.

## Safety

- Never commit `.env*`, `.vercel`, provider keys, email credentials, Blob tokens, or Convex secrets.
- Keep production project IDs, domains, databases, storage, and environment values unchanged during source-only migrations.
- Do not publish private committee application data or internal planning documents.
- Avoid inventing events, committee members, research access, equipment access, outcomes, or institutional claims.
- Preserve accessible controls, reduced-motion behaviour, the public site’s visual identity, and honest empty states.
- Confirm the target Vercel project before any production deployment. A successful local build is not production evidence.
