# Deployment

The pipeline matches the one used by the [OpenEV Data Explorer](https://github.com/open-ev-data/open-ev-data-ui).

## Workflows

| Workflow | Trigger | What it does |
| --- | --- | --- |
| `CI` | Push and pull request to `main` | `npm ci`, lint, unit tests, build |
| `Release` | `CI` succeeded on `main` | Runs `semantic-release`: version, `CHANGELOG.md`, GitHub release, Docker image on GHCR |
| `Deploy to GitHub Pages` | `Release` finished, or manual | Downloads the latest dataset, builds and publishes `dist/` |

Deploy fetches the dataset with `npm run dataset:fetch`, which saves the JSON asset of the latest `open-ev-data-dataset` release to `public/dataset.json` before `npm run build`.

## Versioning

`.releaserc.js` uses Conventional Commits on `main` (and `beta` as prerelease). `feat` bumps the minor version, `fix`, `perf`, `refactor` and `revert` bump the patch, and a breaking change bumps the major. The first release is `1.0.0`. The release commit updates `CHANGELOG.md`, `package.json` and `package-lock.json` with `[skip ci]`.

## Docker

```bash
docker compose -f docker/example/docker-compose.yml up
```

The image `ghcr.io/open-ev-data/open-ev-data-sustainability` is built by `docker/release/scripts/build-docker.sh` during the release and serves the app at `/open-ev-data-sustainability/`. The dataset is downloaded into the image at build time.

## Repository settings required

- **Pages**: Settings, Pages, source set to **GitHub Actions**.
- **Secrets**: `APP_ID` and `PRIVATE_KEY` of the GitHub App used by the release, with the app installed on this repository and allowed to push to `main`.
- **Packages**: after the first release, make the GHCR package public if it should be pulled without authentication.
