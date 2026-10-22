# Surrey Neurotech Society

The public website and committee applications service for Surrey Neurotech Society.

- Website: [surreyneurotechsociety.org](https://surreyneurotechsociety.org)
- Committee applications: the separate `surrey-neurotech-applications` Vercel project
- GitHub: [joshuasknott/surreyneurotech](https://github.com/joshuasknott/surreyneurotech)

The website is an Astro server-rendered application. It uses the existing shared Convex service for published society data and the shared Surrey society packages in this repository. The applications service is an independent Astro application with its own Resend and Vercel Blob integrations.

## Repository layout

```text
apps/
  neurotech/                 # public society website
  neurotech-applications/   # standalone committee recruitment app
packages/
  admin/                     # society configuration and Convex client
  assistant/                 # public assistant server
  ui/                        # shared Astro components
e2e/                         # Neurotech website and application browser checks
scripts/                     # release preparation and brand assets
```

## Local development

Use Node.js 22.12 or newer and npm.

```sh
npm ci
Copy-Item .env.example apps/neurotech/.env.local
npm run dev:neurotech
```

The website runs at `http://127.0.0.1:4323`. To run the applications service instead:

```sh
npm run dev:neurotech-applications
```

It runs at `http://127.0.0.1:4324`.

The applications service has its own environment file:

```powershell
Copy-Item .env.example apps/neurotech-applications/.env.local
```

Set `CONVEX_URL` to the existing shared Convex deployment for local website data. The website renders an empty committee state when the public query is unavailable, so pages remain inspectable without credentials.

## Checks

```sh
npm run typecheck
npm test
npm run build:neurotech
npm run build:neurotech-applications
npm run e2e:site
npm run e2e:applications
```

The applications browser checks use safe local Resend and Blob placeholders and do not send email. Keep real credentials in Vercel or ignored local environment files; never commit them.

## Deployment

The website keeps the existing Vercel project and custom domain. Leave its Vercel project root directory empty (repository root), use `node scripts/build-vercel.mjs neurotech` as the build command, and use `.vercel/output` as the Build Output API directory.

The applications service keeps its separate Vercel project. Set its Vercel project root directory to `apps/neurotech-applications`, use `npm run build` as the build command, and leave the output directory on Vercel's automatic Astro setting.

Required server-side values are listed in [.env.example](.env.example). The shared Convex deployment remains owned by the Surrey AI repository during this staged repository migration; do not create a second Convex deployment from this repository.

## Contributing

Keep society information factual, preserve member-data privacy, and test both phone and desktop layouts. Read [AGENTS.md](AGENTS.md) before changing source or deployment settings. Pull requests should include the relevant typecheck, unit tests, build, and browser-check results.
