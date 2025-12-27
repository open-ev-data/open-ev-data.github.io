---
title: Getting Started
---

# Getting Started with OpenEV Data

Welcome! This guide will help you get started with OpenEV Data, whether you want to use the data, contribute to the project, or integrate the API into your application.

## Choose Your Path

=== "Use the Data"

    **Best for**: Data scientists, researchers, analysts
    
    You can access the data in multiple formats:
    
    1. **Direct Download** (Simplest)
       - Download pre-compiled datasets from [GitHub Releases](https://github.com/open-ev-data/open-ev-data-dataset/releases)
       - Available formats: JSON, CSV, SQLite, PostgreSQL, XML
    
    2. **Clone the Repository**
       ```bash
       git clone https://github.com/open-ev-data/open-ev-data-dataset.git
       cd open-ev-data-dataset
       ```
    
    3. **Browse the Data**
       - Explore the [dataset repository](https://github.com/open-ev-data/open-ev-data-dataset) structure
       - Read the [Schema Reference](../dataset/SCHEMA.md)
    
    **Next Steps**: [Quick Start →](quick-start.md)

=== "Use the API"

    **Best for**: Developers building applications
    
    The REST API provides programmatic access to all vehicle data:
    
    **Base URL**: `https://api.open-ev-data.org/v1`
    
    **Example Request**:
    ```bash
    curl https://api.open-ev-data.org/v1/vehicles/tesla/model_3/2024
    ```
    
    **Features**:
    
    - Fast response times (<50ms globally)
    - RESTful design
    - OpenAPI documentation
    - Filter and search capabilities
    - Pagination support
    
    **Next Steps**: [API Documentation →](../api/index.md)

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

## Prerequisites

Choose based on your path:

=== "Data Users"

    No prerequisites! Just download the files.
    
    **Optional**:
    - SQLite viewer for `.db` files
    - JSON viewer/editor
    - Spreadsheet software for CSV

=== "API Consumers"

    - HTTP client (curl, Postman, or your programming language's HTTP library)
    - API key (coming soon - currently open access)

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

## Installation

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

See the [API Getting Started](../api/GET_STARTED.md) or [Project Setup Guide](../governance/GET_STARTED.md) for detailed development setup.

## Quick Examples

### Query the API

=== "cURL"

    ```bash
    curl https://api.open-ev-data.org/v1/vehicles?make=tesla
    ```

=== "Python"

    ```python
    import requests
    
    response = requests.get('https://api.open-ev-data.org/v1/vehicles/tesla/model_3/2024')
    vehicle = response.json()
    print(f"Range: {vehicle['range']['rated'][0]['range_km']} km")
    ```

=== "JavaScript"

    ```javascript
    fetch('https://api.open-ev-data.org/v1/vehicles/tesla/model_3/2024')
      .then(response => response.json())
      .then(vehicle => {
        console.log(`Range: ${vehicle.range.rated[0].range_km} km`);
      });
    ```

### Load SQLite Database

=== "Python"

    ```python
    import sqlite3
    
    conn = sqlite3.connect('vehicles.db')
    cursor = conn.cursor()
    
    cursor.execute("SELECT * FROM vehicles WHERE make_slug = 'tesla'")
    vehicles = cursor.fetchall()
    ```

=== "Rust"

    ```rust
    use rusqlite::{Connection, Result};
    
    fn main() -> Result<()> {
        let conn = Connection::open("vehicles.db")?;
        
        let mut stmt = conn.prepare("SELECT * FROM vehicles WHERE make_slug = ?")?;
        let vehicles = stmt.query_map(["tesla"], |row| {
            Ok(row.get::<_, String>(0)?)
        })?;
        
        Ok(())
    }
    ```

## Next Steps

Ready to dive deeper? Here are some recommended paths:

<div class="grid cards" markdown>

-   [**Quick Start Guide**](quick-start.md)
    
    Step-by-step tutorial

-   [**API Architecture**](../api/ARCHITECTURE.md)
    
    Understand the API design

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

