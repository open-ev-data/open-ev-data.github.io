---
title: Schema Reference
---

# Dataset Schema Reference

!!! info "Complete Schema Documentation"
    This page provides an overview of the schema. For complete field-by-field documentation, see the [Schema Documentation](https://github.com/open-ev-data/open-ev-data-dataset/blob/main/docs/SCHEMA.md) in the dataset repository.

## Overview

The OpenEV Data schema defines the structure and validation rules for all vehicle specifications in the database. It uses JSON Schema for validation and ensures data consistency across all vehicles.

## Schema Version

Current schema version: **1.0.0**

All vehicle records must include:

```json
{
  "schema_version": "1.0.0"
}
```

## Required Root Fields

Every canonical vehicle record must include:

| Field | Type | Description |
|-------|------|-------------|
| `schema_version` | string | Schema version (e.g., "1.0.0") |
| `make` | object | Manufacturer information |
| `model` | object | Model information |
| `year` | integer | Model year |
| `trim` | object | Trim/grade information |
| `vehicle_type` | string | Vehicle classification |
| `powertrain` | object | Drivetrain and motors |
| `battery` | object | Battery specifications |
| `charge_ports` | array | Physical charge ports |
| `charging` | object | Charging capabilities |
| `range` | object | Range ratings |
| `sources` | array | Data sources |

## Key Field Groups

### Vehicle Identification

```json
{
  "make": {
    "slug": "tesla",
    "name": "Tesla"
  },
  "model": {
    "slug": "model_3",
    "name": "Model 3"
  },
  "year": 2024,
  "trim": {
    "slug": "base",
    "name": "Base"
  },
  "variant": {
    "slug": "long_range",
    "name": "Long Range",
    "kind": "range_upgrade"
  }
}
```

### Battery System

```json
{
  "battery": {
    "pack_capacity_kwh_gross": 82.0,
    "pack_capacity_kwh_net": 75.0,
    "chemistry": "nmc",
    "voltage_nominal_v": 400,
    "thermal_management": "liquid",
    "warranty": {
      "years": 8,
      "km": 192000,
      "capacity_percent": 70
    }
  }
}
```

### Charging Capabilities

```json
{
  "charge_ports": [
    {
      "kind": "combo",
      "connector": "ccs2",
      "location": {
        "side": "left",
        "position": "rear"
      }
    }
  ],
  "charging": {
    "ac": {
      "max_power_kw": 11.0,
      "phases": 3,
      "onboard_charger_kw": 11.0
    },
    "dc": {
      "max_power_kw": 250.0,
      "architecture_voltage_class": "400v",
      "max_current_a": 625,
      "charge_curve": [
        { "soc_percent": 0, "power_kw": 250 },
        { "soc_percent": 50, "power_kw": 250 },
        { "soc_percent": 80, "power_kw": 100 }
      ]
    },
    "protocols": {
      "dc": ["iso_15118_2", "din_70121"],
      "plug_and_charge": true
    }
  }
}
```

### Range and Efficiency

```json
{
  "range": {
    "rated": [
      {
        "cycle": "wltp",
        "range_km": 629,
        "consumption_kwh_per_100km": 13.0
      },
      {
        "cycle": "epa",
        "range_km": 568,
        "consumption_kwh_per_100km": 14.5
      }
    ]
  }
}
```

### Powertrain

```json
{
  "powertrain": {
    "drivetrain": "awd",
    "motors": [
      {
        "position": "front",
        "power_kw": 180,
        "torque_nm": 420,
        "type": "permanent_magnet"
      },
      {
        "position": "rear",
        "power_kw": 220,
        "torque_nm": 480,
        "type": "permanent_magnet"
      }
    ],
    "system_power_kw": 400,
    "system_torque_nm": 900
  }
}
```

### Performance

```json
{
  "performance": {
    "acceleration_0_100_kmh_s": 4.4,
    "acceleration_0_60_mph_s": 4.2,
    "top_speed_kmh": 200,
    "quarter_mile_s": 13.0
  }
}
```

### Dimensions and Weight

```json
{
  "dimensions": {
    "length_mm": 4720,
    "width_mm": 1933,
    "height_mm": 1445,
    "wheelbase_mm": 2875,
    "cargo_capacity_l": 561
  },
  "weight": {
    "curb_kg": 1844,
    "gvwr_kg": 2340,
    "payload_kg": 496
  }
}
```

### V2X Capabilities

```json
{
  "v2x": {
    "v2l": {
      "supported": true,
      "max_power_kw": 3.6,
      "connector": "standard_outlet"
    },
    "v2h": {
      "supported": true,
      "max_power_kw": 9.6
    },
    "v2g": {
      "supported": false
    }
  }
}
```

### Sources

```json
{
  "sources": [
    {
      "type": "oem",
      "title": "Tesla Model 3 Official Specifications",
      "url": "https://www.tesla.com/model3/specs",
      "country": "US",
      "accessed_at": "2025-12-25T00:00:00Z",
      "notes": "Official manufacturer specifications"
    },
    {
      "type": "certification",
      "title": "EPA Certification",
      "url": "https://fueleconomy.gov/...",
      "country": "US",
      "accessed_at": "2025-12-25T00:00:00Z"
    }
  ]
}
```

## Field Types

### String Enums

Many fields use predefined string values:

**Vehicle Types**:
- `sedan`, `suv`, `crossover`, `hatchback`, `coupe`, `wagon`, `van`, `pickup`, `sports_car`

**Drivetrains**:
- `fwd`, `rwd`, `awd`

**Battery Chemistry**:
- `lfp`, `nmc`, `nca`, `lmo`, `solid_state`

**Connectors**:
- `type1`, `type2`, `ccs1`, `ccs2`, `nacs`, `chademo`, `gbt_ac`, `gbt_dc`

**Test Cycles**:
- `wltp`, `epa`, `nedc`, `cltc`, `jc08`

### Units Convention

All measurements use SI or specified units:

| Measurement | Unit | Field Suffix |
|-------------|------|--------------|
| Power | Kilowatts | `_kw` |
| Energy | Kilowatt-hours | `_kwh` |
| Distance | Kilometers | `_km` |
| Distance (short) | Millimeters | `_mm` |
| Weight | Kilograms | `_kg` |
| Voltage | Volts | `_v` |
| Current | Amperes | `_a` |
| Time | Seconds | `_s` |
| Time (long) | Minutes | `_minutes` |
| Torque | Newton-meters | `_nm` |
| Volume | Liters | `_l` |
| Speed | Kilometers per hour | `_kmh` |
| Consumption | kWh per 100 km | `_kwh_per_100km` |

## Validation Rules

### Slugs

- Must match pattern: `^[a-z0-9_]+$`
- No leading/trailing underscores
- Lowercase only

### Required Relationships

- At least one battery capacity (gross or net)
- At least one charge port
- At least one rated range entry
- At least one source
- If variant exists, must reference valid base vehicle

### Data Integrity

- Year must be reasonable (1990-2050)
- Capacities must be positive
- Ranges must be positive
- Dates must be valid ISO 8601
- URLs must be valid format

## Complete Schema

For the complete JSON Schema definition:

[**View schema.json** →](https://github.com/open-ev-data/open-ev-data-dataset/blob/main/schema.json)

For detailed field-by-field documentation:

[**Read Complete Schema Documentation** →](https://github.com/open-ev-data/open-ev-data-dataset/blob/main/docs/SCHEMA.md)

## Related Documentation

<div class="grid cards" markdown>

-   [**Architecture**](architecture.md)
    
    Dataset structure

-   [**Adding a Vehicle**](../../guides/adding-vehicle.md)
    
    Practical guide

-   [**Data Quality**](../../guides/data-quality.md)
    
    Quality standards

-   [**Example Files**](https://github.com/open-ev-data/open-ev-data-dataset/tree/main/example)
    
    Working examples

</div>

