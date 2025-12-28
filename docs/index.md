---
title: OpenEV Data
---

# Welcome to OpenEV Data

<div style="text-align: center; margin: 3rem 0;">
  <img src="assets/images/open-ev-data-logo.svg" alt="OpenEV Data Logo" style="max-width: 400px; width: 100%;" />
</div>

<div class="grid cards" markdown>

-   __Single Source of Truth__

    ---

    The world's most accurate, scientifically validated, and accessible open database of Electric Vehicle specifications.

-   __Built for Performance__

    ---

    High-performance Rust ecosystem with Edge API deployment, providing global low-latency access to data.

-   __Data-as-Code__

    ---

    Version control, strict schema validation, and community review for every data point—from battery chemistry to charging curves.

-   __Open & Collaborative__

    ---

    Community-driven project with contributions from EV enthusiasts, engineers, and manufacturers worldwide.

</div>

## What is OpenEV Data?

OpenEV Data develops and maintains the world's most accurate open database of Electric Vehicle specifications. Unlike fragmented proprietary lists, OpenEV is built on **Data-as-Code** principles, ensuring:

- **Version Control**: Every change is tracked and reviewable
- **Schema Validation**: Strict typing prevents invalid data
- **Community Review**: Multiple eyes on every specification
- **Global Standards**: Support for CCS, NACS, CHAdeMO, GB/T, and more

## Quick Links

<div class="grid cards" markdown>

-   [**Get Started →**](getting-started/index.md)
    
    Learn how to use the dataset or API

-   [**Project Governance →**](governance/index.md)
    
    Learn about project structure and policies

-   [**API Documentation →**](api/index.md)
    
    Explore the REST API documentation

-   [**Dataset Documentation →**](dataset/index.md)
    
    Learn about the EV dataset structure

-   [**Contribute →**](guides/contributing.md)
    
    Help improve the database

</div>

## Project Status

| Component   | Status                                                                                                                                                        |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Website** | [![Website](https://img.shields.io/website?url=https%3A%2F%2Fopen-ev-data.github.io)](https://open-ev-data.github.io)                                         |
| **API**     | [![Status](https://img.shields.io/website?url=https%3A%2F%2Fapi.open-ev-data.org%2Fhealth)](https://github.com/open-ev-data/open-ev-data-api)                 |
| **Dataset** | [![Latest Release](https://img.shields.io/github/v/release/open-ev-data/open-ev-data-dataset)](https://github.com/open-ev-data/open-ev-data-dataset/releases) |

## Repository Structure

OpenEV Data is modular by design to separate concerns between data curation and software engineering.

| Repository                                                                           | Description                                                                 | Tech Stack                         |
| :----------------------------------------------------------------------------------- | :-------------------------------------------------------------------------- | :--------------------------------- |
| [**open-ev-data-dataset**](https://github.com/open-ev-data/open-ev-data-dataset)     | The core database. Contains all vehicle JSONs and validation schemas.       | JSON, JSON Schema                  |
| [**open-ev-data-api**](https://github.com/open-ev-data/open-ev-data-api)             | The high-performance engine. Handles ETL, SQL generation, and the Edge API. | **Rust**, Wasm, Cloudflare Workers |
| [**open-ev-data.github.io**](https://github.com/open-ev-data/open-ev-data.github.io) | Official documentation, guides, and API reference.                          | MkDocs, Material                   |
| [**.github**](https://github.com/open-ev-data/.github)                               | Governance, organization-wide policies, and issue templates.                | Markdown                           |

## Use Cases

=== "Developers"

    Integrate EV specifications into your applications:
    
    - EV comparison tools
    - Range calculators
    - Charging time estimators
    - Route planning with charging stops

=== "Researchers"

    Access structured data for analysis:
    
    - EV market analysis
    - Charging infrastructure planning
    - Battery technology trends
    - Energy consumption studies

=== "Charging Networks"

    Optimize charging infrastructure:
    
    - Vehicle compatibility databases
    - Charging curve optimization
    - Protocol support validation
    - Power requirements planning

## Supported Standards

OpenEV Data standardizes specifications across multiple global charging standards:

- **CCS2** (EU/Global)
- **NACS / J3400** (North America/Tesla)
- **CCS1** (North America Legacy)
- **GB/T** (China)
- **CHAdeMO** (Japan/Legacy)
- **Type 2 / Type 1** (AC Charging)

## Technical Highlights

- **Strict Typing**: All data is validated against rigorous JSON Schemas before merging
- **Deep Merge Architecture**: Hierarchical inheritance model (Base → Year → Trim) ensures DRY data entry
- **Edge Computing**: API deployed globally using Cloudflare Workers, ensuring <50ms latency
- **Rust Core**: All tooling (ETL, Validation, Server) written in Rust for safety and performance

## Docker Compose Example

Create a `docker-compose.yml` file with the following content:

```yaml
name: open-ev-data

services:
  api:
    image: ghcr.io/open-ev-data/ev-server:latest
    container_name: open-ev-data-api
    restart: unless-stopped
    environment:
      DATABASE_URL: /app/vehicles.db
      PORT: 8080
      HOST: 0.0.0.0
      RUST_LOG: info
    ports:
      - "8080:8080"
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:8080/health"]
      interval: 30s
      timeout: 10s
      retries: 3
      start_period: 15s
    init: true
    entrypoint: >
      sh -c "
        echo '[INFO] Getting latest release version...' &&
        LATEST_VERSION=$$(curl -sL https://api.github.com/repos/open-ev-data/open-ev-data-dataset/releases/latest | grep '\"tag_name\":' | cut -d'\"' -f4) &&
        echo \"[INFO] Latest version: $$LATEST_VERSION\" &&
        DOWNLOAD_URL=\"https://github.com/open-ev-data/open-ev-data-dataset/releases/download/$$LATEST_VERSION/open-ev-data-$$LATEST_VERSION.db\" &&
        echo \"[INFO] Downloading from: $$DOWNLOAD_URL\" &&
        curl -fSL -o /app/vehicles.db \"$$DOWNLOAD_URL\" &&
        echo \"[INFO] Database downloaded\" &&
        ls -lh /app/vehicles.db &&
        echo \"[INFO] Starting API server...\" &&
        exec /app/ev-server
      "
```

Run `docker compose up -d --build` to start the API server.

Access the API at `http://localhost:8080/docs`.

## License

This project employs a dual-licensing strategy:

1. **Software (API/CLI)**: Apache License, Version 2.0
2. **Database (Dataset)**: CDLA-Permissive-2.0
3. **Documentation**: CC-BY 4.0

See [License](about/license.md) for details.

