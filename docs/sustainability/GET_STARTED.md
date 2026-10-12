# Getting Started

This guide sets up **OpenEV Data Sustainability** for local development.

## Prerequisites

- **Node.js**: version 22 (the version used by CI).
- **npm**: version 10 or higher.

## Installation

```bash
git clone https://github.com/open-ev-data/open-ev-data-sustainability.git
cd open-ev-data-sustainability
npm ci --legacy-peer-deps
```

`--legacy-peer-deps` is used by CI and Docker as well, because of React 19 peer dependency ranges.

## Development

```bash
npm run dev
```

The app is served at `http://localhost:5173/open-ev-data-sustainability/`.

### Dataset in development

The app loads `public/dataset.json` when it exists. Otherwise, in development only, it fetches the latest dataset release through the proxies in `vite.config.ts`.

To work offline or reproduce production exactly, download the same file the deploy uses:

```bash
npm run dataset:fetch
```

`public/dataset.json` is ignored by git.

## Testing

```bash
npm test                      # unit tests (Vitest)
npx playwright install        # once, to download browsers
npm run test:e2e              # end-to-end tests (Playwright)
```

End-to-end tests intercept `dataset.json` with a small fixture and do not need network access.

## Quality control

```bash
npm run lint
npm run build                 # type-check, bundle and generate the sitemap
```

Commits follow [Conventional Commits](https://www.conventionalcommits.org/); releases are generated from them. See [Deployment](DEPLOYMENT.md).

## Project structure

The project follows **Feature-Sliced Design**. See [Architecture](ARCHITECTURE.md).
