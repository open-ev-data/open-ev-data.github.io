# Page Layouts

This document defines the page-level layout specifications for each route. Component visual specs are in [UI_COMPONENTS.md](UI_COMPONENTS.md). Responsive adaptation rules are in [RESPONSIVE_STRATEGY.md](RESPONSIVE_STRATEGY.md). Design tokens referenced here are defined in [DESIGN_SYSTEM.md](DESIGN_SYSTEM.md).

### Related Documents

| Document                                           | Scope                                                          |
| -------------------------------------------------- | -------------------------------------------------------------- |
| [Design System](DESIGN_SYSTEM.md)                  | Tokens for colors, spacing, typography, shadows                |
| [UI Components](UI_COMPONENTS.md)                  | Component anatomy, states, and **data-driven rendering rules** |
| [Responsive Strategy](RESPONSIVE_STRATEGY.md)      | Breakpoints and viewport-specific behavior                     |
| [Schema Reference](schema/reference_20260216.json) | Required vs optional vehicle data fields                       |

## Table of Contents

- [Global Layout](#global-layout)
- [Home Page](#home-page)
- [Vehicle Detail Page](#vehicle-detail-page)
- [Compare Page](#compare-page)
- [Not Found Page](#not-found-page)
- [Loading and Error States](#loading-and-error-states)

---

## Global Layout

The `AppLayout` wraps all pages and provides the persistent header and optional bottom navigation.

### Desktop Structure

```mermaid
block-beta
  columns 3
  Header["HEADER: OpenEV Data Explorer [Search]"]:3
  Space1:1
  Main["&lt;Outlet /&gt; (Page Content)"]:1
  Space2:1

  style Header fill:#1f2937,stroke:#374151,color:#fff
  style Main fill:#111827,stroke:#374151,color:#fff
  style Space1 fill:none,stroke:none
  style Space2 fill:none,stroke:none
```

### Mobile Structure

```mermaid
block-beta
  columns 1
  Header["HEADER (compact)"]:1
  Main["&lt;Outlet /&gt; (Page Content)"]:1
  Nav["BOTTOM NAV"]:1

  style Header fill:#1f2937,stroke:#374151,color:#fff
  style Main fill:#111827,stroke:#374151,color:#fff
  style Nav fill:#1f2937,stroke:#374151,color:#fff
```

### Header Specs

| Property   | Value                                                     |
| ---------- | --------------------------------------------------------- |
| Height     | `64px` (desktop), `56px` (mobile)                         |
| Background | `--bg-surface-1` with `backdrop-filter: blur(12px)`       |
| Border     | `1px solid var(--border-subtle)` bottom                   |
| Position   | `sticky`, `top: 0`                                        |
| Z-Index    | `--z-sticky`                                              |
| Logo Font  | `--text-lg`, `--weight-bold`, `--text-primary`            |
| Logo Icon  | `⚡` or custom SVG, `--text-accent`                       |
| Padding    | `0 var(--space-6)` (desktop), `0 var(--space-4)` (mobile) |

### Bottom Navigation (Mobile Only)

| Property       | Value                                               |
| -------------- | --------------------------------------------------- |
| Height         | `56px`                                              |
| Background     | `--bg-surface-1` with `backdrop-filter: blur(12px)` |
| Border         | `1px solid var(--border-subtle)` top                |
| Position       | `fixed`, `bottom: 0`                                |
| Z-Index        | `--z-sticky`                                        |
| Icon Size      | `--icon-lg` (`24px`)                                |
| Label Font     | `--text-xs`, `--weight-medium`                      |
| Active Color   | `--text-accent`                                     |
| Inactive Color | `--text-tertiary`                                   |

---

## Home Page

**Route**: `/`
**Component**: `HomePage`
**Reference**: [A01 Desktop](reference/A01-home-page.png) · [M01 Mobile](reference/M01-mobile-home-page.png)

### Desktop Layout

```mermaid
block-beta
  columns 4
  Header["HEADER"]:4
  block:Content:4
    columns 2
    Filter["FILTER PANEL (240px fixed)"]
    block:Right
        columns 1
        TopBar["All Cards | Search"]
        block:Grid
            columns 4
            Card1["Card"]
            Card2["Card"]
            Card3["Card"]
            Card4["Card"]
            Card5["Card"]
            Card6["Card"]
            Card7["Card"]
            Card8["Card"]
        end
        Pagination["[Pagination]"]
    end
  end

  style Header fill:#1f2937,stroke:#374151,color:#fff
  style Filter fill:#1f2937,stroke:#374151,color:#fff
  style TopBar fill:#374151,stroke:#4b5563,color:#fff
  style Pagination fill:#374151,stroke:#4b5563,color:#fff
  style Card1 fill:#1f2937,stroke:#4b5563,color:#fff
  style Card2 fill:#1f2937,stroke:#4b5563,color:#fff
  style Card3 fill:#1f2937,stroke:#4b5563,color:#fff
  style Card4 fill:#1f2937,stroke:#4b5563,color:#fff
  style Card5 fill:#1f2937,stroke:#4b5563,color:#fff
  style Card6 fill:#1f2937,stroke:#4b5563,color:#fff
  style Card7 fill:#1f2937,stroke:#4b5563,color:#fff
  style Card8 fill:#1f2937,stroke:#4b5563,color:#fff
```

### Mobile Layout

```mermaid
block-beta
  columns 1
  Header["HEADER"]:1
  Filters["[Filters & Sort ▾]"]:1
  block:List
    columns 1
    Card1["[Img] Name | Stats | [Compare]"]:1
    Card2["[Img] Name | Stats | [Compare]"]:1
    More["...more cards"]:1
  end
  Nav["BOTTOM NAV"]:1

  style Header fill:#1f2937,stroke:#374151,color:#fff
  style Filters fill:#374151,stroke:#4b5563,color:#fff
  style Nav fill:#1f2937,stroke:#374151,color:#fff
  style Card1 fill:#1f2937,stroke:#4b5563,color:#fff
  style Card2 fill:#1f2937,stroke:#4b5563,color:#fff
```

### Page Component Hierarchy

```mermaid
graph TD
    HomePage --> FilterPanel
    HomePage --> ContentHeader
    ContentHeader --> ViewToggle
    ContentHeader --> SearchInput
    HomePage --> VehicleGrid
    VehicleGrid --> VehicleCard
    HomePage --> Pagination
```

### Spec Details

| Property             | Desktop                                           | Mobile                      |
| -------------------- | ------------------------------------------------- | --------------------------- |
| Main layout          | `display: grid; grid-template-columns: 240px 1fr` | Single column               |
| Content area padding | `--space-6`                                       | `--space-4`                 |
| Card grid gap        | `--space-6`                                       | `--space-4`                 |
| Grid columns         | `repeat(auto-fill, minmax(240px, 1fr))`           | `1fr`                       |
| Secondary search     | Top-right of content area                         | Hidden (uses header search) |
| Filter position      | Sticky sidebar                                    | Collapsible at top          |

### Comparison Overlay (Active)

**Reference**: [A02 Desktop](reference/A02-home-page-compare-open.png) · [M02 Mobile](reference/M02-mobile-home-page-compare-open.png)

When the user opens the comparison view from the Home Page:

**Desktop**: A panel slides in from the right side, overlaying ~40% of the viewport width. The card grid content is visible but dimmed behind the panel.

```mermaid
block-beta
  columns 3
  Filter["FILTER PANEL"]:1
  Grid["Vehicle Grid (dimmed)"]:1
  Panel["COMPARISON PANEL (~40% width)"]:1

  style Filter fill:#1f2937,stroke:#374151,color:#fff
  style Grid fill:#111827,stroke:#374151,color:#bbb
  style Panel fill:#1f2937,stroke:#374151,color:#fff,stroke-width:2px
```

**Mobile**: Full-screen overlay replacing the card list. The comparison panel takes 100% of the viewport with a "Close" button at top-right.

| Property     | Desktop                             | Mobile                                |
| ------------ | ----------------------------------- | ------------------------------------- |
| Panel width  | `~40vw`, min `380px`                | `100vw`                               |
| Animation    | `slide-in-right`, `--duration-slow` | `slide-in-right` or full opacity fade |
| Overlay bg   | `hsla(0,0%,0%,0.4)` behind panel    | None (full takeover)                  |
| Close button | `×` ghost button, top-right         | "Close" text button, top-right        |

---

## Vehicle Detail Page

**Route**: `/vehicle/:code`
**Component**: `VehicleDetailPage`
**Reference**: [A03 Desktop](reference/A03-view-one-vehicle.png) · [M03 Mobile](reference/M03-mobile-view-one-vehicle.png)

### Desktop Layout

```mermaid
block-beta
  columns 4
  Header["HEADER"]:4
  Sidebar["Sidebar"]:1
  Main["Main Content"]:3

  block:SidebarContent
    Back["← Back"]:1
    Image["[Vehicle Image]"]:1
    Highlights["Highlights List"]:1
    Technology["Technology"]:1
  end

  block:MainContent
    Title["Make Model Trim"]:1
    Tabs["Overview | Charging | Range | Specs"]:1
    Pills["Price | Range | Battery | 0-100"]:1
    block:Charts
        columns 2
        Chart1["Charging Curve"]:1
        Chart2["Range Estimates"]:1
    end
  end

  style Header fill:#1f2937,stroke:#374151,color:#fff
  style Sidebar fill:#1f2937,stroke:#374151,color:#fff
  style Main fill:#111827,stroke:#374151,color:#fff
```

### Mobile Layout

```mermaid
block-beta
  columns 1
  Header["HEADER"]:1
  Back["← Back"]:1
  Title["BYD Seal AWD Performance"]:1
  Image["[Vehicle Image]"]:1
  Pills["Price | Range | Battery | 0-100"]:1
  Tabs["Overview | Charging..."]:1
  Highlights["Highlights"]:1
  Charts["Range Estimates"]:1
  Compare["Compare (Sticky)"]:1
  Nav["BOTTOM NAV"]:1

  style Header fill:#1f2937,stroke:#374151,color:#fff
  style Compare fill:#10b981,stroke:#059669,color:#fff
  style Nav fill:#1f2937,stroke:#374151,color:#fff
```

### Page Component Hierarchy

```mermaid
graph TD
    VehicleDetailPage --> BackButton
    VehicleDetailPage --> VehicleHeader
    VehicleHeader --> VehicleName
    VehicleHeader --> VehicleTags
    VehicleDetailPage --> VehicleImage
    VehicleDetailPage --> SpecsPills
    VehicleDetailPage --> TabBar
    VehicleDetailPage --> TabContent
    TabContent --> OverviewTab
    OverviewTab --> HighlightsList
    OverviewTab --> ChargingOverviewTable
    TabContent --> ChargingCurveTab
    TabContent --> RangeScenariosTab
    TabContent --> FullSpecsTab
    VehicleDetailPage --> CompareButton
```

> [!IMPORTANT]
> **Data-driven tab visibility**: The tab bar only renders tabs whose underlying data exists for the current vehicle. The Overview tab is always present. Charging Curve requires `charging.dc_charge_curve`. Range Scenarios requires `range.real_world[]`. Full Specs is always present but each section within it collapses when empty. See [Data-Driven Rendering Principle](UI_COMPONENTS.md#data-driven-rendering-principle) for implementation details.

### Spec Details

| Property         | Desktop                             | Mobile                     |
| ---------------- | ----------------------------------- | -------------------------- |
| Layout           | 2-column: sidebar 280px + main area | Single column              |
| Sidebar bg       | `--bg-surface-1`                    | —                          |
| Image position   | Sidebar, centered                   | Full width, below title    |
| Image max height | `200px`                             | `200px`                    |
| Spec pills       | Horizontal row in main area         | Horizontal scroll          |
| Tab bar position | Below spec pills in main            | Below spec pills           |
| Charts layout    | Side by side (2 cols)               | Stacked vertically         |
| Compare button   | Top-right area, ghost style         | Sticky bottom, primary CTA |

---

## Compare Page

**Route**: `/compare`
**Component**: `ComparePage`

The standalone Compare Page provides a full-page comparison experience. This differs from the comparison panel overlay on the Home Page.

### Layout

```mermaid
block-beta
  columns 1
  Header["HEADER"]:1
  block:Page
    Title["Comparison (X)"]
    block:Grid
        columns 3
        V1["Vehicle 1 \n [Image] \n Tesla M3"]
        V2["Vehicle 2 \n [Image] \n BYD Seal"]
        V3["Vehicle 3 \n [Image] \n Porsche T"]

        R1["Range | Price | 0-100"]
        R2["Range | Price | 0-100"]
        R3["Range | Price | 0-100"]

        Chart1["[Radar] \n [Bars]"]
        Chart2["[Radar] \n [Bars]"]
        Chart3["[Radar] \n [Bars]"]
    end
  end

  style Header fill:#1f2937,stroke:#374151,color:#fff
  style Page fill:#111827,stroke:#374151,color:#fff
  style V1 fill:#1f2937,stroke:#374151,color:#fff
  style V2 fill:#1f2937,stroke:#374151,color:#fff
  style V3 fill:#1f2937,stroke:#374151,color:#fff
```

### Comparison Data Sections

All comparison rows are **data-driven**. A row only renders if at least one of the compared vehicles has data for that field. If a vehicle is missing a field that others have, display "—" in that cell. See [rendering rules](UI_COMPONENTS.md#rendering-rules).

1. **Key Metrics Table**: Range, Price, 0-100 km/h, Battery — rows filtered by data availability
2. **Radar Charts**: Only shown if enough metrics exist for a meaningful polygon (≥ 3 axes)
3. **Efficiency Bars**: Only shown if `efficiency.energy_consumption_wh_per_km` exists for at least one vehicle
4. **Charging Comparison**: AC max power, DC max power, architecture — from required `charging` object

### Spec Details

| Property          | Value                                                       |
| ----------------- | ----------------------------------------------------------- |
| Max vehicles      | 3                                                           |
| Column min width  | `200px` (desktop), `160px` (mobile)                         |
| Column header bg  | `--bg-glass`                                                |
| Row border        | `--border-subtle`                                           |
| Best value        | `--text-accent`, `--weight-bold`                            |
| Radar chart size  | `160px × 160px` (desktop), `120px × 120px` (mobile)         |
| Radar colors      | `--chart-cyan`, `--chart-green`, `--chart-teal` per vehicle |
| Remove button (×) | `ghost` button, top-right of column header                  |

---

## Not Found Page

**Route**: `*`
**Component**: `NotFoundPage`

### Layout

```mermaid
block-beta
  columns 1
  Header["HEADER"]:1
  Space1:1
  Icon["⚠️ (404 Icon)"]:1
  Title["Page Not Found"]:1
  Msg["The page you're looking for doesn't exist."]:1
  Btn["[ Go to Home ]"]:1
  Space2:1

  style Header fill:#1f2937,stroke:#374151,color:#fff
  style Icon fill:none,stroke:none,color:#eab308
  style Btn fill:#10b981,stroke:#059669,color:#fff
```

### Specs

| Property   | Value                                 |
| ---------- | ------------------------------------- |
| Layout     | Flex column, centered both axes       |
| Min height | `calc(100vh - header height)`         |
| Icon       | `--icon-xl` (32px), `--color-warning` |
| Title      | `--text-3xl`, `--weight-bold`         |
| Message    | `--text-base`, `--text-secondary`     |
| Button     | `primary` variant, `lg` size          |

---

## Loading and Error States

### Initial Loading (Full Page)

When the application first loads and fetches the vehicle dataset:

```mermaid
block-beta
  columns 1
  Header["HEADER"]:1
  Space1:1
  Spinner["(Spinner lg)"]:1
  Text["Loading vehicle data..."]:1
  Space2:1

  style Header fill:#1f2937,stroke:#374151,color:#fff
  style Spinner fill:none,stroke:none
```

### Skeleton Loading (Cards)

While data is being processed/filtered, card skeletons maintain layout stability:

```mermaid
block-beta
  columns 1
  Image["[Image Placeholder (pulse)]"]:1
  Title["[Title Placeholder]"]:1
  Stats["[Stats Placeholder]"]:1
  Btn["[Button Placeholder]"]:1

  style Image fill:#1f2937,stroke:none,color:#6b7280
  style Title fill:#1f2937,stroke:none,color:#6b7280
  style Stats fill:#1f2937,stroke:none,color:#6b7280
  style Btn fill:#1f2937,stroke:none,color:#6b7280
```

### Skeleton Specs

| Property          | Value                                                                     |
| ----------------- | ------------------------------------------------------------------------- |
| Background        | `--bg-surface-2`                                                          |
| Animated gradient | `linear-gradient(90deg, transparent, hsla(210,20%,30%,0.2), transparent)` |
| Animation         | `pulse` keyframe, `1.5s infinite`                                         |
| Border radius     | Matches target element                                                    |
| Height            | Matches expected content height                                           |

### Error State (API Failure)

```mermaid
block-beta
  columns 1
  Header["HEADER"]:1
  Space1:1
  Icon["⚠️ (Alert Icon)"]:1
  Title["Unable to load vehicle data"]:1
  Msg["Please check your connection and try again."]:1
  Btn["[ Retry ]"]:1
  Space2:1

  style Header fill:#1f2937,stroke:#374151,color:#fff
  style Icon fill:none,stroke:none,color:#ef4444
  style Btn fill:#10b981,stroke:#059669,color:#fff
```

| Property     | Value                             |
| ------------ | --------------------------------- |
| Component    | `ErrorFallback` from `shared/ui/` |
| Icon         | Alert triangle, `--color-warning` |
| Title        | `--text-xl`, `--weight-semibold`  |
| Message      | `--text-base`, `--text-secondary` |
| Retry button | `primary` variant                 |
