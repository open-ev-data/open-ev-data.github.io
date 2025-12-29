---
title: Getting Started
---

# Getting Started with OpenEV Data

Welcome! This guide will help you get started with OpenEV Data, whether you want to use the data, contribute to the project, or run the API locally.

## Choose Your Path

=== "Use the Data"

    **Best for**: Data scientists, researchers, analysts, developers
    
    Access pre-compiled EV datasets directly from our GitHub Releases:
    
    **Download from**: [GitHub Releases](https://github.com/open-ev-data/open-ev-data-dataset/releases)
    
    **Available Formats**:
    
    | Format         | Best For                                       |
    | :------------- | :--------------------------------------------- |
    | **CSV**        | Spreadsheets, data analysis, pandas            |
    | **JSON**       | Web apps, JavaScript/TypeScript projects       |
    | **SQLite**     | Local queries, mobile apps, embedded databases |
    | **PostgreSQL** | Production databases, cloud deployments        |
    | **XML**        | Enterprise integrations, legacy systems        |
    
    Simply download the format you need - no installation required!
    
    **Next Steps**: [Quick Start →](quick-start.md)

=== "Fork & Customize"

    **Best for**: Projects needing custom vehicle data
    
    Fork the repository to create and maintain your own vehicle database:
    
    1. **Fork the Repository**
       - Go to [open-ev-data-dataset](https://github.com/open-ev-data/open-ev-data-dataset)
       - Click the "Fork" button
    
    2. **Clone Your Fork**
       ```bash
       git clone https://github.com/YOUR_USERNAME/open-ev-data-dataset.git
       cd open-ev-data-dataset
       npm install
       ```
    
    3. **Add Your Custom Data**
       - Add vehicle JSON files to `src/` following the [Schema Reference](../dataset/SCHEMA.md)
       - Run validation: `npm run validate`
    
    4. **Generate Your Dataset**
       - Use the ETL pipeline to generate output files
       - Configure GitHub Actions for automated releases
    
    **Next Steps**: [Dataset Documentation →](../dataset/index.md)

=== "Contribute"

    **Best for**: EV enthusiasts, engineers, manufacturers
    
    Help us maintain the most accurate EV database:
    
    **Ways to Contribute**:
    
    1. **Add Vehicle Data**
       - Submit specifications for new EVs
       - Check the [Dataset Documentation](../dataset/index.md)
    
    2. **Correct Existing Data**
       - Report inaccuracies
       - Provide reliable sources
    
    3. **Improve Documentation**
       - Fix typos and clarify instructions
       - Add examples and tutorials
    
    4. **Develop Features**
       - Work on the API or ETL pipeline
       - Check the [API Documentation](../api/index.md)
    
    **Next Steps**: [Contributing Guide →](../guides/contributing.md)

## Quick Start: Using the Data

### Download Your Preferred Format

1. Go to [GitHub Releases](https://github.com/open-ev-data/open-ev-data-dataset/releases)
2. Download the latest release in your preferred format
3. Start using the data immediately!

### Example: Load SQLite Database

=== "Python"

    ```python
    import sqlite3
    
    # Download the SQLite file from releases first
    conn = sqlite3.connect('OpenEV Data (SQLite).db')
    cursor = conn.cursor()
    
    # List all Tesla vehicles
    cursor.execute("SELECT * FROM vehicles WHERE make_slug = 'tesla'")
    vehicles = cursor.fetchall()
    
    for vehicle in vehicles:
        print(vehicle)
    ```

=== "Rust"

    ```rust
    use rusqlite::{Connection, Result};
    
    fn main() -> Result<()> {
        let conn = Connection::open("OpenEV Data (SQLite).db")?;
        
        let mut stmt = conn.prepare(
            "SELECT make_slug, model_slug FROM vehicles WHERE make_slug = ?"
        )?;
        
        let vehicles = stmt.query_map(["tesla"], |row| {
            Ok((row.get::<_, String>(0)?, row.get::<_, String>(1)?))
        })?;
        
        for vehicle in vehicles {
            println!("{:?}", vehicle?);
        }
        
        Ok(())
    }
    ```

### Example: Load CSV Data

=== "Python (pandas)"

    ```python
    import pandas as pd
    
    # Download the CSV file from releases first
    df = pd.read_csv('OpenEV Data (CSV).csv')
    
    # Filter Tesla vehicles
    tesla_vehicles = df[df['make_slug'] == 'tesla']
    print(tesla_vehicles[['model_name', 'variant_name', 'battery_capacity_kwh']])
    ```

=== "JavaScript"

    ```javascript
    import { parse } from 'csv-parse/sync';
    import { readFileSync } from 'fs';
    
    const csv = readFileSync('OpenEV Data (CSV).csv', 'utf-8');
    const vehicles = parse(csv, { columns: true });
    
    const teslaVehicles = vehicles.filter(v => v.make_slug === 'tesla');
    console.log(teslaVehicles);
    ```

### Example: Load JSON Data

=== "Python"

    ```python
    import json
    
    # Download the JSON file from releases first
    with open('OpenEV Data (JSON).json') as f:
        vehicles = json.load(f)
    
    # Filter Tesla vehicles
    tesla = [v for v in vehicles if v['make_slug'] == 'tesla']
    for vehicle in tesla:
        print(f"{vehicle['model_name']} - {vehicle['variant_name']}")
    ```

=== "JavaScript"

    ```javascript
    import vehicles from './OpenEV Data (JSON).json';
    
    const teslaVehicles = vehicles.filter(v => v.make_slug === 'tesla');
    teslaVehicles.forEach(v => {
        console.log(`${v.model_name} - ${v.variant_name}`);
    });
    ```

## Running the API Locally

> [!NOTE]
> There is no public API hosted online. To use the API, you need to run it locally using Docker or build it from source.

### Quick Start with Docker

The fastest way to run the API locally:

```bash
git clone https://github.com/open-ev-data/open-ev-data-dataset.git
cd open-ev-data-dataset
docker-compose up -d
```

This will:

- Download the latest dataset SQLite database
- Start the API server on http://localhost:8080

Access the API:

```bash
curl http://localhost:8080/api/v1/vehicles
```

Stop the stack:

```bash
docker-compose down
```

### Build from Source

For API development:

```bash
git clone https://github.com/open-ev-data/open-ev-data-api.git
cd open-ev-data-api
cargo build
cargo run
```

See the [API Documentation](../api/index.md) for more details.

## Prerequisites

Choose based on your path:

=== "Data Users"

    No prerequisites! Just download the files from [GitHub Releases](https://github.com/open-ev-data/open-ev-data-dataset/releases).
    
    **Optional**:
    
    - SQLite viewer for `.db` files (e.g., [DB Browser for SQLite](https://sqlitebrowser.org/))
    - JSON viewer/editor
    - Spreadsheet software for CSV (Excel, LibreOffice Calc, Google Sheets)
    - PostgreSQL client for `.sql` files

=== "Local API"

    - [Docker](https://www.docker.com/) and [Docker Compose](https://docs.docker.com/compose/)
    
    Or for building from source:
    
    - [Rust](https://www.rust-lang.org/) 1.80+
    - [Cargo](https://doc.rust-lang.org/cargo/)

=== "Contributors"

    **For Dataset Contributors**:
    
    - [Git](https://git-scm.com/)
    - [Node.js](https://nodejs.org/) 18+
    - Text editor (VS Code recommended)
    - Understanding of JSON
    
    **For API Developers**:
    
    - [Rust](https://www.rust-lang.org/) 1.80+
    - [Cargo](https://doc.rust-lang.org/cargo/)
    - Understanding of REST APIs
    
    **For Documentation**:
    
    - [Python](https://www.python.org/) 3.13+
    - [Poetry](https://python-poetry.org/)

## Development Installation

=== "Dataset Development"

    ```bash
    git clone https://github.com/open-ev-data/open-ev-data-dataset.git
    cd open-ev-data-dataset
    npm install
    npm run validate
    ```

=== "API Development"

    ```bash
    git clone https://github.com/open-ev-data/open-ev-data-api.git
    cd open-ev-data-api
    cargo build
    cargo test
    ```

=== "Documentation Development"

    ```bash
    git clone https://github.com/open-ev-data/open-ev-data.github.io.git
    cd open-ev-data.github.io
    poetry install
    poetry run mkdocs serve
    ```

## Multi-Repository Workspace

For contributors working across multiple repositories, we provide a pre-configured workspace:

```bash
mkdir open-ev-data
cd open-ev-data
git clone https://github.com/open-ev-data/open-ev-data-dataset.git
git clone https://github.com/open-ev-data/open-ev-data-api.git
git clone https://github.com/open-ev-data/open-ev-data.github.io.git
git clone https://github.com/open-ev-data/.github.git
```

Then open the workspace file:

```bash
code .github/open-ev-data.code-workspace
```

**Benefits**:

- Unified search across all repositories
- Cross-repository navigation
- Consistent settings
- Organized sidebar

See the [Project Setup Guide](../governance/GET_STARTED.md) for detailed development setup.

## Next Steps

Ready to dive deeper? Here are some recommended paths:

<div class="grid cards" markdown>

-   [**Quick Start Guide**](quick-start.md)
    
    Step-by-step tutorial

-   [**Schema Reference**](../dataset/SCHEMA.md)
    
    Understand the data structure

-   [**Contributing Guide**](../guides/contributing.md)
    
    Start contributing

-   [**Dataset Documentation**](../dataset/index.md)
    
    Learn about the dataset

</div>

## Get Help

- **Issues**: [GitHub Issues](https://github.com/open-ev-data/.github/issues)
- **Discussions**: [GitHub Discussions](https://github.com/orgs/open-ev-data/discussions)
- **Documentation**: You're reading it!

## Community

Join our community:

- Follow development on [GitHub](https://github.com/open-ev-data)
- Read our [Code of Conduct](../governance/CODE_OF_CONDUCT.md)
- Check project updates in the [Changelogs](../changelog-api.md)
