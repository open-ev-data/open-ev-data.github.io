---
title: OpenEV Data
---

# Welcome to OpenEV Data

<div style="text-align: center; margin: 3rem 0;">
  <img src="assets/images/logo.svg" alt="OpenEV Data Logo" style="max-width: 400px; width: 100%;" />
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

-   [**Contribute →**](guides/contributing.md)
    
    Help improve the database

-   [**API Reference →**](documentation/api/endpoints.md)
    
    Integrate OpenEV into your app

-   [**View Dataset →**](https://github.com/open-ev-data/open-ev-data-dataset)
    
    Browse the raw data

</div>

## Project Status

| Component | Status |
|-----------|--------|
| **Website** | [![Website](https://img.shields.io/website?url=https%3A%2F%2Fopen-ev-data.github.io)](https://open-ev-data.github.io) |
| **API** | [![Status](https://img.shields.io/website?url=https%3A%2F%2Fapi.open-ev-data.org%2Fhealth)](https://github.com/open-ev-data/open-ev-data-api) |
| **Dataset** | [![Latest Release](https://img.shields.io/github/v/release/open-ev-data/open-ev-data-dataset)](https://github.com/open-ev-data/open-ev-data-dataset/releases) |

## Repository Structure

OpenEV Data is modular by design to separate concerns between data curation and software engineering.

| Repository | Description | Tech Stack |
|:-----------|:------------|:-----------|
| [**open-ev-data-dataset**](https://github.com/open-ev-data/open-ev-data-dataset) | The core database. Contains all vehicle JSONs and validation schemas. | JSON, JSON Schema |
| [**open-ev-data-api**](https://github.com/open-ev-data/open-ev-data-api) | The high-performance engine. Handles ETL, SQL generation, and the Edge API. | **Rust**, Wasm, Cloudflare Workers |
| [**open-ev-data.github.io**](https://github.com/open-ev-data/open-ev-data.github.io) | Official documentation, guides, and API reference. | MkDocs, Material |
| [**.github**](https://github.com/open-ev-data/.github) | Governance, organization-wide policies, and issue templates. | Markdown |

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

## License

This project employs a dual-licensing strategy:

1. **Software (API/CLI)**: Apache License, Version 2.0
2. **Database (Dataset)**: CDLA-Permissive-2.0
3. **Documentation**: CC-BY 4.0

See [License](about/license.md) for details.

