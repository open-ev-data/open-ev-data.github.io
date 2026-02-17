# Getting Started

Welcome to the **OpenEV Data UI** project! This guide will help you set up your development environment and get the application running locally.

## Prerequisites

- **Node.js**: Version 20 or higher.
- **npm**: Version 10 or higher.

## Installation

1.  **Clone the repository**:

    ```bash
    git clone https://github.com/open-ev-data/open-ev-data-ui.git
    cd open-ev-data-ui
    ```

2.  **Install dependencies**:
    We recommend using `npm ci` to ensure you install the exact versions specified in `package-lock.json`.
    ```bash
    npm ci
    ```
    > **Note**: If you encounter peer dependency issues (common with React 19), you can use `npm ci --legacy-peer-deps`.

## Development

To start the development server:

```bash
npm run dev
```

This will start the Vite server at `http://localhost:5173`.

### Data Fetching in Development

In development mode, the application uses a **local proxy** configured in `vite.config.ts`. This allows the app to fetch the latest dataset from GitHub releases without encountering CORS errors, simulating the production environment where the dataset is served locally.

## Testing

We use **Vitest** for unit testing and **Playwright** for end-to-end (E2E) testing.

- **Run Unit Tests**:

  ```bash
  npm test
  ```

- **Run E2E Tests**:

  ```bash
  # Install Playwright browsers first
  npx playwright install

  # Run tests (headless)
  npm run test:e2e

  # Run tests with UI
  npm run test:e2e:ui
  ```

## Building for Production

To build the application for production:

```bash
npm run build
```

The output will be in the `dist/` directory.

### Production Dataset Strategy

During the build process (specifically in the CI/CD pipeline), the latest vehicle dataset is automatically downloaded and bundled into the `public/` directory. The production app then fetches this local `dataset.json` file, ensuring fast load times and zero CORS issues.

## Quality Control

- **Linting**:

  ```bash
  npm run lint
  ```

  We use ESLint to enforce code quality and stylistic consistency.

- **Formatting**:
  The project uses Prettier. It's recommended to install the Prettier extension for VS Code to format on save.

## Project Structure

This project follows the **Feature-Sliced Design (FSD)** methodology:

- `src/app/`: Global app setup (providers, router, styles).
- `src/widgets/`: Compositional layers (Header, Footer, complex page blocks).
- `src/features/`: User scenarios (Search, Filter, Compare).
- `src/entities/`: Business entities (Vehicle, Brand).
- `src/shared/`: Reusable UI components, libs, and config.
