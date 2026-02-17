# Responsive Strategy

This document defines the responsive design strategy for the Open EV Data UI. Visual tokens referenced here are defined in [DESIGN_SYSTEM.md](DESIGN_SYSTEM.md). Component-level specs are in [UI_COMPONENTS.md](UI_COMPONENTS.md).

### Related Documents

| Document | Scope |
| --- | --- |
| [Design System](DESIGN_SYSTEM.md) | Spacing, typography, and breakpoint tokens |
| [UI Components](UI_COMPONENTS.md) | Component specs and data-driven rendering rules |
| [Page Layouts](PAGE_LAYOUTS.md) | Page composition using these responsive strategies |
| [Architecture](ARCHITECTURE.md) | FSD layers and routing |

## Table of Contents

- [Responsive Philosophy](#responsive-philosophy)
- [Breakpoints](#breakpoints)
- [Layout Strategy per Viewport](#layout-strategy-per-viewport)
- [Grid System](#grid-system)
- [Component Adaptations](#component-adaptations)
- [Typography Scaling](#typography-scaling)
- [Touch Interactions](#touch-interactions)
- [Performance Considerations](#performance-considerations)

---

## Responsive Philosophy

1. **Mobile-first CSS**: base styles target mobile; larger viewports layer on via `min-width` media queries
2. **Content-driven breakpoints**: standard breakpoints with component-specific overrides when content demands it
3. **Progressive enhancement**: mobile gets a fully functional core experience; desktop gets enhanced visualizations
4. **Avoid hiding information**: content is reorganized, never removed — optional fields that don't exist in the data are simply not rendered (see [Data-Driven Rendering](UI_COMPONENTS.md#data-driven-rendering-principle))
5. **Touch-native on mobile**: larger touch targets, bottom navigation bar

---

## Breakpoints

Defined in `src/shared/styles/breakpoints.css`:

| Token | Value | Name | Typical Devices |
| --- | --- | --- | --- |
| `--bp-sm` | `640px` | Small | Large phones, landscape |
| `--bp-md` | `768px` | Medium | Tablets portrait |
| `--bp-lg` | `1024px` | Large | Tablets landscape, small laptops |
| `--bp-xl` | `1280px` | Extra large | Standard desktops |
| `--bp-2xl` | `1440px` | Wide | Wide monitors |

> [!IMPORTANT]
> CSS custom properties cannot be used in media queries. Use the raw pixel values in `@media` declarations. The `breakpoints.css` file serves as documentation.

### Media Query Pattern (Mobile-First)

```css
/* Mobile first — base styles are mobile */
@media (min-width: 640px)  { /* sm */ }
@media (min-width: 768px)  { /* md */ }
@media (min-width: 1024px) { /* lg */ }
@media (min-width: 1280px) { /* xl */ }
@media (min-width: 1440px) { /* 2xl */ }
```

---

## Layout Strategy per Viewport

### Mobile (< 640px)

Reference: [M01](reference/M01-mobile-home-page.png), [M02](reference/M02-mobile-home-page-compare-open.png), [M03](reference/M03-mobile-view-one-vehicle.png)

| Aspect | Behavior |
| --- | --- |
| **Layout** | Single-column, full-width |
| **Header** | Compact — logo + full-width search bar |
| **Filter** | Collapsed "Filters & Sort" accordion at top |
| **Cards** | Stacked vertically, horizontal inner layout (image left, info right) |
| **Comparison** | Full-screen overlay, 3 columns scroll horizontally |
| **Vehicle Detail** | Full-width vertical flow, image top, specs below |
| **Navigation** | Bottom tab bar: Home, Search, Favorites, More |

### Tablet (640px – 1023px)

| Aspect | Behavior |
| --- | --- |
| **Layout** | 2-column card grid |
| **Filter** | Collapsible sidebar or floating panel |
| **Comparison** | Side panel overlay, 60% screen width |
| **Vehicle Detail** | 2-column: image+highlights left, data right |

### Desktop (1024px – 1439px)

Reference: [A01](reference/A01-home-page.png), [A02](reference/A02-home-page-compare-open.png), [A03](reference/A03-view-one-vehicle.png)

| Aspect | Behavior |
| --- | --- |
| **Layout** | Sidebar (240px) + content area |
| **Header** | Full-width, logo left, centered search |
| **Filter** | Persistent left sidebar, always visible |
| **Cards** | 3–4 column grid |
| **Comparison** | Right overlay panel (~40% width), slides in |
| **Vehicle Detail** | Sidebar (back+image+highlights) + main (tabs+charts) |
| **Navigation** | Header-only, no bottom bar |

### Wide Desktop (≥ 1440px)

| Aspect | Behavior |
| --- | --- |
| **Content** | Max width `1400px`, centered |
| **Cards** | 5-column grid |
| **Comparison** | Wider overlay with more chart space |

---

## Grid System

```css
.cardGrid {
  display: grid;
  gap: var(--space-6);
  grid-template-columns: 1fr;
}

@media (min-width: 640px)  { .cardGrid { grid-template-columns: repeat(2, 1fr); } }
@media (min-width: 1024px) { .cardGrid { grid-template-columns: repeat(3, 1fr); } }
@media (min-width: 1280px) { .cardGrid { grid-template-columns: repeat(4, 1fr); } }
@media (min-width: 1440px) { .cardGrid { grid-template-columns: repeat(5, 1fr); } }
```

### Container Widths

| Viewport | Max Width | Side Padding |
| --- | --- | --- |
| Mobile | `100%` | `--space-4` |
| Tablet | `100%` | `--space-6` |
| Desktop | `1200px` | `--space-8` |
| Wide | `1400px` | `--space-8` |

---

## Component Adaptations

### Header

| Viewport | Behavior |
| --- | --- |
| Mobile | Logo (icon only) + full-width search bar |
| Desktop | Logo (full) + centered search bar + right actions |

### FilterPanel

| Viewport | Behavior |
| --- | --- |
| Mobile | Hidden by default. "Filters & Sort" accordion/bottom sheet |
| Desktop | Persistent sidebar (240px), sticky positioning |

### VehicleCard

| Viewport | Card Layout | Grid Columns |
| --- | --- | --- |
| Mobile | Horizontal (image 30%, info 70%) | 1 |
| Tablet | Vertical (image top, info below) | 2 |
| Desktop | Vertical | 3–5 |

### CompareTable

| Viewport | Behavior |
| --- | --- |
| Mobile | Full-screen overlay. Columns scroll horizontally |
| Tablet | 60% width side panel |
| Desktop | 40% width right panel, slides in from right |

### Vehicle Detail

| Viewport | Layout |
| --- | --- |
| Mobile | Single column: Back → Title → Image → Specs → Tabs → Content → Compare (sticky) |
| Desktop | Left sidebar (back+image+highlights), Right (title+tabs+specs+charts) |

### Navigation

| Viewport | Type |
| --- | --- |
| Mobile | Bottom tab bar: 🏠 Home, 🔍 Search, ☆ Favorites, ⚡ More |
| Desktop | Header-only navigation |

---

## Typography Scaling

| Token | Desktop | Mobile |
| --- | --- | --- |
| `--text-4xl` | `48px` | `32px` |
| `--text-3xl` | `36px` | `28px` |
| `--text-2xl` | `30px` | `24px` |
| `--text-xl` | `24px` | `20px` |
| `--text-lg` | `20px` | `18px` |
| `--text-base` | `16px` | `16px` |

Use `clamp()` for fluid scaling:

```css
:root {
  --text-2xl: clamp(1.5rem, 1.2rem + 1vw, 1.875rem);
  --text-3xl: clamp(1.75rem, 1.4rem + 1.2vw, 2.25rem);
  --text-4xl: clamp(2rem, 1.5rem + 1.5vw, 3rem);
}
```

### Spacing Adjustments

| Token Usage | Desktop | Mobile |
| --- | --- | --- |
| Card padding | `--space-6` | `--space-3` to `--space-4` |
| Grid gap | `--space-6` | `--space-4` |
| Section gap | `--space-10` | `--space-6` |
| Page padding | `--space-8` | `--space-4` |

---

## Touch Interactions

| Interaction | Mobile Behavior |
| --- | --- |
| Card tap | Navigate to detail or show quick-action |
| Compare button tap | Add to comparison, show toast |
| Filter accordion tap | Toggle open/close |
| Pull to refresh | Trigger TanStack Query refetch |
| Bottom nav tap | Navigate to section |

> [!TIP]
> All touch targets must have a minimum size of `44px × 44px` per WCAG guidelines.

---

## Performance Considerations

| Strategy | Implementation |
| --- | --- |
| Image optimization | Appropriate sizes per viewport, `srcset`/`sizes` |
| Lazy loading | `loading="lazy"` for below-fold images |
| Virtualization | `react-window` for 400+ vehicle lists |
| Reduced motion | Honor `prefers-reduced-motion: reduce` |
| CSS containment | `contain: layout style paint` on card containers |
| Font loading | `font-display: swap` for Inter |
