---
title: Dataset Overview
---

# Dataset Overview

The OpenEV Data Dataset is the core of the project - a canonical, open dataset of electric vehicle specifications following a Layered Canonical Dataset (LCD) architecture.

## Quick Information

| | |
|---|---|
| **License** | CDLA-Permissive-2.0 |
| **Format** | JSON (layered structure) |
| **Validation** | JSON Schema |
| **Repository** | [open-ev-data-dataset](https://github.com/open-ev-data/open-ev-data-dataset) |

## What is the Dataset?

The dataset provides **structured, versioned, and community-maintained** EV specifications authored as **layered JSON fragments** and compiled into **canonical, fully-expanded vehicle records**.

### Key Features

- **Layered Structure**: Base → Year → Variant inheritance
- **DRY Principle**: No repeated data
- **Schema Validation**: Strict type checking
- **Version Controlled**: Git-based
- **Community Reviewed**: Pull request workflow
- **Multi-Format Output**: JSON, SQLite, PostgreSQL, CSV, XML

## Repository Structure

The dataset follows a hierarchical directory structure:

```text
src/
  <make_slug>/
    <model_slug>/
      base.json                    # Shared specifications
      <year>/
        <vehicle_slug>.json        # Base vehicle for year
        <vehicle_slug>_<variant_slug>.json  # Variant
```

### Example: BYD Seal

```text
src/
  byd/
    seal/
      base.json                    # Common to all years
      2023/
        seal.json                  # Base 2023 model
        seal_performance.json      # Performance variant
      2024/
        seal.json                  # Base 2024 model
        seal_performance.json      # Performance variant
```

## Data Coverage

The dataset aims to cover:

### Vehicle Identity

- Make, model, year
- Trim and variant configurations
- Market availability

### Battery System

- Chemistry (LFP, NMC, etc.)
- Capacity (gross/net)
- Voltage and cell count
- Thermal management
- Warranty information
- Preconditioning support

### Charging Infrastructure

- Charge ports (Type 1, Type 2, CCS1, CCS2, NACS, CHAdeMO, GB/T)
- Port location and features
- Connector types

### Charging Capabilities

- AC power, phases, onboard charger specs
- DC fast charging peak power
- Voltage class (400V, 800V)
- Charging curves
- Supported protocols

### Bidirectional Charging (V2X)

- V2L (Vehicle-to-Load)
- V2H (Vehicle-to-Home)
- V2G (Vehicle-to-Grid)
- Power limits and protocols

### Range and Efficiency

- Rated cycles (WLTP, EPA, NEDC, CLTC, JC08)
- Real-world estimates
- Energy consumption

### Powertrain

- Motor configuration
- Power and torque
- Drivetrain (FWD, RWD, AWD)
- Transmission

### Performance

- Acceleration (0-100 km/h, 0-60 mph)
- Top speed
- Quarter mile times

### Physical Specifications

- Dimensions (length, width, height)
- Weight (curb, GVWR)
- Cargo capacity
- Towing capacity

### Wheels and Tires

- Wheel sizes
- Tire specifications
- Recommended pressures

### Market Data

- Availability status
- Markets by country
- Pricing (MSRP)

### Software

- Operating system
- OTA update support

### Sources and Metadata

- Verifiable sources
- Data quality indicators
- Contributors

## Complete Documentation

The dataset has comprehensive documentation in its own repository:

<div class="grid cards" markdown>

-   [**Architecture Documentation**](architecture.md)
    
    Complete architectural details

-   [**Schema Reference**](schema.md)
    
    Field-by-field documentation

-   [**Example Vehicle**](https://github.com/open-ev-data/open-ev-data-dataset/tree/main/example)
    
    Minimal example structure

-   [**Browse Dataset**](https://github.com/open-ev-data/open-ev-data-dataset/tree/main/src)
    
    Explore the data

</div>

## Use Cases

### Research

- EV market analysis
- Charging infrastructure planning
- Battery technology trends
- Energy consumption studies

### Applications

- EV comparison tools
- Range calculators
- Charging time estimators
- Route planners

### APIs

- Backend data source
- Automotive applications
- Charging network integration

### Education

- Learning about EV technology
- Understanding specifications
- Comparing technologies

## Download Pre-Built Datasets

Pre-compiled datasets are available in multiple formats:

[**Download from Releases** →](https://github.com/open-ev-data/open-ev-data-dataset/releases)

Available formats:

- `vehicles.json` - Complete canonical dataset
- `vehicles.db` - SQLite database
- `vehicles.sql` - PostgreSQL schema + data
- `vehicles.csv` - Flattened tabular format
- `vehicles.xml` - XML representation

## Contributing Data

Help expand and maintain the database:

1. Read the [Contributing Guide](../../guides/contributing.md)
2. Review the [Data Quality Standards](../../guides/data-quality.md)
3. Follow the [Adding a Vehicle](../../guides/adding-vehicle.md) guide
4. Submit a pull request

## Next Steps

<div class="grid cards" markdown>

-   [**Architecture Details**](architecture.md)
    
    Technical architecture

-   [**Schema Reference**](schema.md)
    
    Complete field documentation

-   [**Quick Start**](../../getting-started/quick-start.md)
    
    Start using the data

-   [**Add a Vehicle**](../../guides/adding-vehicle.md)
    
    Contribute data

</div>

