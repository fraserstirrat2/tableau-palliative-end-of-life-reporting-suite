# MSG5 — Tableau Worksheets

This folder documents the worksheets used to assemble the **Last 6 Months of Life by Setting** dashboard.

The completed evidence confirms a compact architecture: four analytical worksheets plus the reporting-suite navigation/help components.

## Analytical worksheets

| Worksheet | Role | Evidence file |
| --- | --- | --- |
| **MSG - Settings Breakdown (Bar)** | Stacked bar for the **Numbers** view using the four supplied bed-day measures | `01-MSG5-Settings-Breakdown-Numbers.png` |
| **MSG - Settings Breakdown (Bar) (2)** | Stacked bar for the **Percentages** view using the four supplied percentage measures | `02-MSG5-Settings-Breakdown-Percentages.png` |
| **MSG - Bed Days by Setting** | Detailed table for absolute bed-day values | `03-MSG5-Settings-Table-Numbers.png` |
| **MSG - Bed Days by Setting %** | Detailed table for percentage distribution | `04-MSG5-Settings-Table-Percentages.png` |

### Numbers stacked bar

![MSG5 Numbers bar worksheet](01-MSG5-Settings-Breakdown-Numbers.png)

The screenshot shows:

- **Columns:** Measure Values
- **Rows:** Financial Year
- filters including Financial Year, Council Area selection, `BedDaysView_Filter` and Measure Names;
- Measure Values populated with Community, Community Hospital, Large Hospital and Palliative bed-day fields;
- Measure Names used for colour/setting separation;
- Possible Bed days and Deaths on the tooltip/detail layer.

### Percentages stacked bar

![MSG5 Percentages bar worksheet](02-MSG5-Settings-Breakdown-Percentages.png)

This worksheet uses the supplied `% Community`, `% Community/Hospital`, `% Large Hospital` and `% Palliative` fields directly. This is important evidence that the main percentage display does not recreate the upstream percentages in Tableau.

### Numbers table

![MSG5 Numbers table worksheet](03-MSG5-Settings-Table-Numbers.png)

The table uses Financial Year on rows, Measure Names on columns and Measure Values as text so the same four setting totals can be read numerically.

### Percentages table

![MSG5 Percentages table worksheet](04-MSG5-Settings-Table-Percentages.png)

The percentage table mirrors the same architecture with the four supplied percentage fields.

## Shared interface worksheets

The dashboard also uses the shared reporting-suite components:

| Evidence file | Role |
| --- | --- |
| `05-home-icon.png` | Home navigation worksheet and tooltip behaviour |
| `06-info-icon.png` | Information view explaining purpose, settings, controls, interpretation and caveats |
| `07-help-icon.png` | Help worksheet / help icon implementation |
| `08-go-to-icon.png` | Go To worksheet / navigation-link implementation |

### Information view

The Information evidence has been prepared for public portfolio use and provides an important part of the dashboard story: the end user is given definitions and interpretation guidance inside the reporting product rather than being expected to infer the indicator from the chart alone.

![MSG5 Information view](06-info-icon.png)

The view explains the four settings, Numbers / Percentages control, financial-year and Council Area context, how to read the chart/table, tooltip use and key interpretation caveats.

The Home, Help and Go To screenshots are retained as supporting implementation evidence because they show how the dashboard participates in the consistent wider reporting-suite navigation pattern.

## Why this worksheet structure works

The architecture deliberately separates Numbers and Percentages at worksheet level while presenting them as one dashboard-level interaction:

```text
Bed Days parameter
      ↓
BedDaysView_Filter
      ↓
Numbers worksheet pair
        OR
Percentages worksheet pair
```

This keeps formatting and measure selection straightforward while giving users one consistent reporting experience.

## Evidence rule

The purpose of these screenshots is to prove the implementation, not to publish the full managed workbook. Public analytical evidence remains Scotland-level and excludes source data, workbooks/extracts, internal paths, credentials and restricted operational material.
