# Architecture

OpenEV Data Sustainability is a static single-page application. It shares its stack, tooling and conventions with the [OpenEV Data Explorer](https://github.com/open-ev-data/open-ev-data-ui); see its [Architecture](https://github.com/open-ev-data/open-ev-data-ui/blob/main/docs/ARCHITECTURE.md) for the general reasoning behind Feature-Sliced Design.

## Data flow

```text
open-ev-data-dataset (latest release)
        |  npm run dataset:fetch (deploy, Docker)
        v
public/dataset.json  ->  dist/dataset.json  ->  browser
        |
        v
useVehicles (TanStack Query)  ->  selected vehicle + usage profile
        |
        v
pure calculators (energy, charging, cost)  ->  widgets
```

There is no API call at runtime. In production the app fetches the bundled `dataset.json`; in development it falls back to the latest GitHub release through Vite proxies when the file is missing.

## Layers

| Layer | Contents |
| --- | --- |
| `app/` | Providers (Helmet, Query, Theme, Usage profile), router, base layout |
| `pages/sustainability` | Composes the flow and the `useSustainabilityModel` hook |
| `widgets/` | `EnergyPanel`, `ChargingPanel`, `CostPanel`, `EnergyTechnologies`, `SustainabilitySummary`, `LayoutHeader`, `LayoutFooter`, `AboutModal` |
| `features/` | `vehicle-selector`, `usage-profile`, `energy-calculator`, `charging-calculator`, `cost-calculator` |
| `entities/vehicle` | Dataset types, API access, helpers and vehicle UI |
| `shared/` | UI kit, theme, formatting, SEO, tokens and config |

Imports only go downward. Calculators are pure functions with no React dependency, which keeps them easy to test; a calculator returns `null` whenever an input is missing.

## Theming

Design tokens live in `src/shared/styles/tokens.css`. The dark palette is the default; `:root[data-theme='light']` overrides the tokens for the light theme. An inline script in `index.html` applies the stored or system preference before first paint, and `ThemeProvider` keeps it in sync. Components must use tokens and never hard-coded colors.

## URL state

The selected vehicle is stored in the `vehicle` query parameter (the vehicle `unique_code`), so a configuration can be shared as a link. The usage profile is stored in `localStorage`.

## Hosting on GitHub Pages

The app is served from `/open-ev-data-sustainability/`. Unknown paths hit `public/404.html`, which redirects to the app with a `?p=` parameter that `index.html` restores.
