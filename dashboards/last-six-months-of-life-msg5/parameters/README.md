# MSG5 — Parameters and User Controls

This folder will document the parameter/control logic used by the **Last 6 Months of Life by Setting** dashboard.

## Bed Days

The main dashboard control is **Bed Days**, with two user-facing states:

1. **Numbers**
2. **Percentages**

The remaining parameter screenshot should be added here so the case study can show the actual Tableau configuration rather than relying only on a written description.

### Reporting role

The control determines which version of the analytical display is active:

```text
Bed Days = Numbers
    ↓
Absolute bed-day bar + table
```

```text
Bed Days = Percentages
    ↓
Percentage-distribution bar + table
```

A calculated field named **BedDaysView_Filter** is visible in the workbook evidence and appears to participate in this switching logic. Its exact formula will be documented in the Calculated Fields section once the screenshot is supplied.

## Council Area

Council Area is a reporting filter rather than the central Numbers/Percentages parameter. It allows the same dashboard structure to be reused across the available reporting geographies.

## Evidence to add

Suggested parameter/control evidence:

```text
01-bed-days-parameter.png
02-council-area-filter.png   # only if useful as implementation evidence
```

The goal is to document how the dashboard works, not to duplicate screenshots that are already obvious from the finished dashboard view.
