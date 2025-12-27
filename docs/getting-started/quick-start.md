---
title: Quick Start
---

# Quick Start Guide

This guide will get you up and running with OpenEV Data in 5 minutes.

## Option 1: Use Pre-Built Datasets

The fastest way to get started is to download pre-compiled datasets.

### Step 1: Download

Go to the [latest release](https://github.com/open-ev-data/open-ev-data-dataset/releases/latest) and download your preferred format:

- `vehicles.json` - Complete canonical dataset
- `vehicles.db` - SQLite database
- `vehicles.sql` - PostgreSQL schema + data
- `vehicles.csv` - Flattened tabular format
- `vehicles.xml` - XML representation

### Step 2: Use the Data

=== "JSON"

    ```python
    import json
    
    with open('vehicles.json', 'r') as f:
        data = json.load(f)
    
    print(f"Total vehicles: {data['vehicle_count']}")
    
    tesla_vehicles = [v for v in data['vehicles'] 
                      if v['make']['slug'] == 'tesla']
    print(f"Tesla vehicles: {len(tesla_vehicles)}")
    ```

=== "SQLite"

    ```python
    import sqlite3
    
    conn = sqlite3.connect('vehicles.db')
    cursor = conn.cursor()
    
    cursor.execute("""
        SELECT make_slug, model_slug, year, 
               battery_pack_capacity_kwh_net
        FROM vehicles 
        WHERE battery_pack_capacity_kwh_net > 75
    """)
    
    for row in cursor.fetchall():
        print(row)
    ```

=== "CSV"

    ```python
    import pandas as pd
    
    df = pd.read_csv('vehicles.csv')
    
    print(df[['make', 'model', 'year', 'range_wltp_km']].head(10))
    
    avg_range = df.groupby('make')['range_wltp_km'].mean()
    print(avg_range)
    ```

## Option 2: Use the REST API

Query the API directly without downloading anything.

### Step 1: Make a Request

=== "cURL"

    ```bash
    curl https://api.open-ev-data.org/v1/vehicles/tesla/model_3/2024 | jq
    ```

=== "Python"

    ```python
    import requests
    
    url = "https://api.open-ev-data.org/v1/vehicles/tesla/model_3/2024"
    response = requests.get(url)
    vehicle = response.json()
    
    print(f"Make: {vehicle['make']['name']}")
    print(f"Model: {vehicle['model']['name']}")
    print(f"Range: {vehicle['range']['rated'][0]['range_km']} km")
    ```

=== "JavaScript"

    ```javascript
    const url = 'https://api.open-ev-data.org/v1/vehicles/tesla/model_3/2024';
    
    fetch(url)
      .then(response => response.json())
      .then(vehicle => {
        console.log(`Make: ${vehicle.make.name}`);
        console.log(`Model: ${vehicle.model.name}`);
        console.log(`Range: ${vehicle.range.rated[0].range_km} km`);
      });
    ```

### Step 2: Explore Endpoints

List all Tesla vehicles:

```bash
curl https://api.open-ev-data.org/v1/vehicles?make=tesla
```

Search for EVs with specific range:

```bash
curl "https://api.open-ev-data.org/v1/vehicles?min_range_km=500"
```

Get all manufacturers:

```bash
curl https://api.open-ev-data.org/v1/makes
```

## Option 3: Clone and Build Locally

For contributors or developers who want to work with the source data.

### Step 1: Clone Repository

```bash
git clone https://github.com/open-ev-data/open-ev-data-dataset.git
cd open-ev-data-dataset
```

### Step 2: Install Dependencies

```bash
npm install
```

### Step 3: Validate Data

```bash
npm run validate
```

### Step 4: Explore the Data

Browse the `src/` directory to see the layered structure:

```
src/
  tesla/
    model_3/
      base.json           # Shared specifications
      2024/
        model_3.json      # Base 2024 trim
        model_3_long_range.json  # Long Range variant
```

## Common Use Cases

### Compare Vehicle Specifications

=== "Python"

    ```python
    import requests
    
    makes = ['tesla', 'byd', 'nissan']
    
    for make in makes:
        url = f"https://api.open-ev-data.org/v1/vehicles?make={make}"
        response = requests.get(url)
        vehicles = response.json()['vehicles']
        
        avg_range = sum(v['range']['rated'][0]['range_km'] 
                       for v in vehicles) / len(vehicles)
        
        print(f"{make.title()}: {avg_range:.0f} km average range")
    ```

### Find Compatible Charging Stations

=== "Python"

    ```python
    import requests
    
    url = "https://api.open-ev-data.org/v1/vehicles/tesla/model_3/2024"
    vehicle = requests.get(url).json()
    
    charge_ports = vehicle['charge_ports']
    
    for port in charge_ports:
        print(f"Port: {port['connector']}")
        print(f"Location: {port['location']['side']} {port['location']['position']}")
        print(f"Kind: {port['kind']}")
        print()
    ```

### Calculate Charging Time

=== "Python"

    ```python
    import requests
    
    url = "https://api.open-ev-data.org/v1/vehicles/byd/seal/2024"
    vehicle = requests.get(url).json()
    
    dc_charging = vehicle['charging']['dc']
    
    print(f"Max DC Power: {dc_charging['max_power_kw']} kW")
    print(f"Voltage Class: {dc_charging['architecture_voltage_class']}")
    
    if 'charge_time' in dc_charging:
        for time_spec in dc_charging['charge_time']:
            print(f"{time_spec['from_soc']}% → {time_spec['to_soc']}%: "
                  f"{time_spec['time_minutes']} minutes")
    ```

## Next Steps

<div class="grid cards" markdown>

-   [**API Documentation**](../api/index.md)
    
    Complete API reference

-   [**Dataset Documentation**](../dataset/index.md)
    
    Learn about the dataset structure

-   [**Contributing Guide**](../guides/contributing.md)
    
    Help improve the database

-   [**Project Setup**](../governance/GET_STARTED.md)
    
    Complete development environment setup

</div>

## Troubleshooting

### API Returns Empty Results

Check if the vehicle exists:

```bash
curl https://api.open-ev-data.org/v1/makes
```

Verify the correct slugs (lowercase, underscores):

```bash
curl https://api.open-ev-data.org/v1/vehicles?make=tesla
```

### Database File Won't Open

Ensure you have SQLite 3.45+ installed:

```bash
sqlite3 --version
```

Download the file again if corrupted:

```bash
wget https://github.com/open-ev-data/open-ev-data-dataset/releases/latest/download/vehicles.db
```

### Validation Fails

Check Node.js version:

```bash
node --version  # Should be 18+
```

Reinstall dependencies:

```bash
rm -rf node_modules package-lock.json
npm install
```

## Get Help

Still stuck? We're here to help:

- [GitHub Issues](https://github.com/open-ev-data/.github/issues)
- [Discussions](https://github.com/orgs/open-ev-data/discussions)
- [Documentation](../index.md)

