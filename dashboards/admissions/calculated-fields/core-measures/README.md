# Core Analytical Measures

This folder contains the two primary derived measures exposed through the Admissions Dashboard Trend Selector:

- Admissions per Death
- Average Length of Stay

## Admissions per Death

This measure is calculated from the reusable parameter-selected activity measures rather than from a fixed source field.

Conceptually:

```text
Admissions per Death = Selected Admissions / Selected Deaths
```

The Tableau calculation first checks whether Selected Deaths is zero and returns null in that case. This prevents divide-by-zero results and ensures the measure always follows the active Time Window selection.

[View calculation screenshot](01-admissions-per-death.png)

## Average Length of Stay

Average Length of Stay is the second main measure available through the Trend Selector and responds to the same dashboard filter and time-window context.

[View calculation screenshot](02-average-length-of-stay.png)

## Why these are separated from the selected activity measures

The selected activity calculations answer **which period-specific source measure should be used**. The core analytical measures then build the reporting metric from those selected values.

That separation makes the workbook easier to reason about and allows the same derived measure to work across all five analytical periods.
