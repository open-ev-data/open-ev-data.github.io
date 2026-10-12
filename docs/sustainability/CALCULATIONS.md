# Calculations

All figures come from the fields of the OpenEV Data dataset and the values entered by the user. See the dataset [Schema](https://github.com/open-ev-data/open-ev-data-dataset/blob/main/docs/SCHEMA.md) for field definitions.

## Energy consumption

Consumption in Wh/km is resolved in this order:

1. `efficiency.energy_consumption_wh_per_km`, when reported and the range basis is **Automatic**.
2. Derived: `battery.pack_capacity_kwh_net * 1000 / range_km`, using the best homologated range (WLTP, EPA, CLTC, NEDC, JC08, other, in that order). The user can pick a specific cycle.

When the value is derived, the interface says so and names the cycle. If neither is possible, the result is "Insufficient data".

```text
annual_km      = distance x (365 | 12 | 1)     for day | month | year
kWh/100 km     = Wh/km / 10
kWh/year       = Wh/km x annual_km / 1000
kWh/month      = kWh/year / 12
```

At the time of writing no vehicle in the dataset reports `energy_consumption_wh_per_km`, so every value is derived. Homologated ranges are typically optimistic, so derived consumption is lower than real-world use.

## Charging

Uses `battery.pack_capacity_kwh_net` and `charging.ac.max_power_kw` or `charging.dc.max_power_kw`, depending on the charger type.

```text
energy_needed   = battery_capacity x (target_soc - initial_soc)
effective_power = min(charger_power, vehicle_max_power)
charging_time   = energy_needed / effective_power
```

Limitations: power is assumed constant. DC charging slows down as the battery fills, so DC times are a lower bound. Charging losses are not modeled. Times reported by the manufacturer (`charging.charging_time`) are shown separately when present.

## Cost

The electricity price is always entered by the user; a price of 0 means "not informed" and hides every cost.

```text
cost_per_100km = kWh/100 km x price
cost_per_month = kWh/month  x price
cost_per_year  = kWh/year   x price
cost_per_charge = energy_needed x price
```

Fees, taxes beyond the entered price, tariff changes and charging losses are not included.

## Energy technologies

V2L, V2H, V2G, chemistry, capacity, heat pump and DC architecture are read from `v2x`, `battery` and `charging.dc`. A missing field is shown as "Not reported", which is different from "Not supported" (an explicit `supported: false`).

## Out of scope

CO2 emissions are not calculated in this version.
