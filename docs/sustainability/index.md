<div align="center">
  <img src="https://raw.githubusercontent.com/open-ev-data/.github/bd1f96d4c236e7c1dc43a33535fc9f065f9b152e/assets/open-ev-data-logo.svg" alt="OpenEV Data Logo" width="200" />
</div>

# OpenEV Data Sustainability

> Turn electric vehicle specifications into real-world energy use: consumption, charging time, running costs and energy technologies.

[![License: Apache 2.0](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://github.com/open-ev-data/open-ev-data-sustainability/blob/main/LICENSE)
[![Version](https://img.shields.io/github/v/release/open-ev-data/open-ev-data-sustainability?label=version)](https://github.com/open-ev-data/open-ev-data-sustainability/releases)
[![CI](https://github.com/open-ev-data/open-ev-data-sustainability/actions/workflows/ci.yml/badge.svg)](https://github.com/open-ev-data/open-ev-data-sustainability/actions/workflows/ci.yml)

## Overview

A static web application that reads the same `dataset.json` as the [OpenEV Data Explorer](https://github.com/open-ev-data/open-ev-data-ui) and answers a different question. The Explorer tells you **what a vehicle is**; Sustainability tells you **what its data means in everyday energy use**.

It needs no backend, database or API at runtime. Values the dataset does not report are shown as unavailable and are never guessed.

## Documentation

- **[Get Started](GET_STARTED.md)** — Setup, development and testing.
- **[Architecture](ARCHITECTURE.md)** — Project structure and data flow.
- **[Calculations](CALCULATIONS.md)** — Formulas, data sources and limitations.
- **[Deployment](DEPLOYMENT.md)** — CI, release, GitHub Pages and Docker.
- **[Contributing](https://github.com/open-ev-data/.github/blob/main/CONTRIBUTING.md)** — How to contribute to the project.

The visual identity follows the Explorer's [Design System](https://github.com/open-ev-data/open-ev-data-ui/blob/main/docs/DESIGN_SYSTEM.md), extended with a light theme.

## Features

- **Vehicle selection**: search, or pick make, model, year and version.
- **Usage profile**: distance, electricity price, state of charge and charger power.
- **Energy consumption**: kWh per 100 km, per month and per year.
- **Charging simulator**: energy needed, effective power and charging time.
- **Cost estimator**: cost per 100 km, month, year and charge.
- **Energy technologies**: V2L, V2H, V2G, battery chemistry, heat pump and charging architecture.
- **Sustainability summary**: the key figures in one dashboard.
- **Dark and light themes**, responsive from mobile to desktop.

## Tech Stack

- **Framework**: [React](https://react.dev/) + [Vite](https://vitejs.dev/)
- **Language**: [TypeScript](https://www.typescriptlang.org/)
- **Styling**: [CSS Modules](https://github.com/css-modules/css-modules) with design tokens
- **Data**: [TanStack Query](https://tanstack.com/query/latest)
- **Charts**: [Recharts](https://recharts.org/)
- **Testing**: [Vitest](https://vitest.dev/) (unit) + [Playwright](https://playwright.dev/) (E2E)

## License

This project is licensed under the **Apache License 2.0**. See [LICENSE](https://github.com/open-ev-data/open-ev-data-sustainability/blob/main/LICENSE) for full terms.

## Acknowledgments

Part of the **OpenEV Data** initiative. Special thanks to all contributors building the open standard for EV specifications.
