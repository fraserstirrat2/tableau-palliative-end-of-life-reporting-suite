# Last 6 Months of Life by Setting (MSG5) — Tableau Implementation

This page documents how the supplied MSG Indicator 5 aggregate output is presented in Tableau.

Compared with the Admissions Dashboard, MSG5 is a more compact implementation. Its technical value is in **clear parameter-driven presentation, coordinated chart/table behaviour, geography selection, filtering, contextual tooltips, information design and accurate translation of a governed source indicator**, rather than in a large calculation layer.

## Dashboard architecture

The evidence confirms that the dashboard combines:

- a stacked bar chart showing setting-level distribution by financial year;
- a detailed yearly table;
- a **Council Area** parameter for reporting geography;
- a **Bed Days** parameter for switching between Numbers and Percentages;
- calculated fields supporting geography selection and view switching;
- shared Home, Go To, Help and Information worksheets;
- tooltips containing additional contextual measures including Deaths and Possible Bed days.

The chart and table are designed to respond together so the user sees one consistent analytical state.

## Bed Days parameter

The main reporting control is **Bed Days**, configured as an integer parameter with a fixed list:

| Stored value | Display value |
| ---: | --- |
| `1` | Numbers |
| `2` | Percentages |

The screenshot confirms **Numbers** as the current value and the workbook-opening behaviour as **Current value**.

![Bed Days parameter](parameters/01-bed-days.png)

This means a simple user-facing dropdown drives the internal worksheet-selection logic without exposing numeric parameter codes to the user.

## Council Area parameter

The **Council Area** parameter is a string list. The supplied configuration shows **Scotland** as the current value and includes the available Council Area reporting geographies.

![Council Area parameter](parameters/01-council-area.png)

Two calculated fields support this control:

- `Council Area`
- `Is Selected Council (Filter)`

Together they compare the selected parameter value with the source geography field and handle the Scotland national state explicitly.

## Numbers view

### Stacked bar — `MSG - Settings Breakdown (Bar)`

![MSG5 Numbers bar worksheet](worksheets/01-MSG5-Settings-Breakdown-Numbers.png)

The worksheet evidence confirms:

- **Columns:** Measure Values
- **Rows:** Financial Year
- filters including Financial Year, the Council Area selection, `BedDaysView_Filter`, Council Area and Measure Names;
- **Measure Values:** Community Bed days, Community/Hospital Bed days, Large Hospital Bed days and Palliative Bed days;
- **Measure Names** controlling the setting colours;
- Possible Bed days and Deaths added to the Marks/tooltip layer.

The Numbers bar therefore uses the supplied aggregate bed-day measures directly.

### Detailed table — `MSG - Bed Days by Setting`

![MSG5 Numbers table worksheet](worksheets/03-MSG5-Settings-Table-Numbers.png)

The table uses:

- **Columns:** Measure Names
- **Rows:** Financial Year
- **Text:** Measure Values
- the same four source-supplied bed-day measures;
- `BedDaysView_Filter` and Council Area selection logic so it stays aligned with the active dashboard state.

## Percentages view

### Stacked bar — `MSG - Settings Breakdown (Bar) (2)`

![MSG5 Percentages bar worksheet](worksheets/02-MSG5-Settings-Breakdown-Percentages.png)

The Percentage bar uses the supplied percentage measures directly:

- `% Community`
- `% Community/Hospital`
- `% Large Hospital`
- `% Palliative`

This confirms that Tableau is presenting the upstream percentage output rather than rebuilding those four formulas in the main visual layer.

### Detailed table — `MSG - Bed Days by Setting %`

![MSG5 Percentages table worksheet](worksheets/04-MSG5-Settings-Table-Percentages.png)

The table mirrors the same four percentage measures by Financial Year and remains tied to the selected Council Area and Percentages state.

## Coordinated view switching

The workbook contains separate Numbers and Percentages worksheet pairs rather than forcing both formats into a single visual.

`BedDaysView_Filter` is a lightweight helper calculation that returns the current Bed Days parameter value. The relevant worksheet pair can therefore be filtered to the correct state while the user experiences one dashboard-level selector.

At reporting level the design is:

```text
Bed Days = Numbers (1)
        ↓
Numbers bar + Numbers table
```

```text
Bed Days = Percentages (2)
        ↓
Percentage bar + Percentage table
```

This is a simple implementation choice that keeps formatting and measure logic clean while presenting a single coherent dashboard to the user.

## Council Area selection logic

The Council Area parameter is not just a visible dropdown. Supporting calculations determine whether the underlying source geography matches the selected parameter state.

The evidence shows two layers:

1. `Council Area` — a direct comparison between the parameter and source Council Area field, with a guard for the `Select` state;
2. `Is Selected Council (Filter)` — an explicit Scotland branch plus the selected-area comparison.

This allows the same dashboard structure to be reused for the national Scotland view and the governed local reporting views in the managed workbook.

The public portfolio remains restricted to Scotland-level output.

## Tooltip design

The bar worksheets add **Possible Bed days** and **Deaths** to the tooltip layer.

In the supplied Scotland Percentages dashboard, hovering 2021/22 shows:

- Financial Year: 2021/22
- Community: 89.70%
- Deaths: 58,441
- Possible Bed days: 10,665,483

This gives users context behind the proportion without overcrowding the main visual.

## Dashboard states

The final dashboard evidence includes two public-safe Scotland states:

### Numbers

![MSG5 Scotland Numbers](dashboard-screenshots/01-L6MOL-Scotland-Level-Dashboard-Overview-Numbers.png)

### Percentages

![MSG5 Scotland Percentages](dashboard-screenshots/02-L6MOL-Scotland-Level-Dashboard-Overview-Percentages.png)

The same legend, financial-year ordering, Council Area selection and navigation components are retained between states.

## Shared interface worksheets

The dashboard uses the reporting-suite navigation/help convention:

- `Discovery home`
- `Discovery Go To`
- `Discovery Help`
- `Discovery Info`

Evidence was supplied for these components. The Home, Go To and Help worksheets are suitable as technical implementation evidence. The Information worksheet screenshot itself contains an explicit internal distribution warning, so that raw screenshot should not be published in the public repository; its analytical content is documented textually instead.

## Calculated fields

The supplied evidence confirms four relevant calculated/helper fields:

- `Council Area`
- `Is Selected Council (Filter)`
- `BedDaysView_Filter`
- `KPI - Community`

The main chart/table measures are source fields rather than extra Tableau calculations. See [Calculated Fields](calculated-fields/README.md).

## Information panel

The managed Information panel explains:

- that the dashboard presents the last six months of life across Community, Community Hospital, Large Hospital and Hospice / Palliative Care;
- that Bed Days can be shown as total numbers or percentages;
- that data are shown by financial year and can be filtered by Council Area;
- how to read the stacked bar and detailed table;
- that users can hover for detailed values;
- that the indicator represents the proportion of time spent in different settings during the final six months of life;
- that Community includes care at home and care homes;
- that linked hospital activity and death records underpin the indicator;
- that source completeness, reporting differences and service configuration need to be considered when interpreting results.

## Why this implementation is useful

The end-user interaction is deliberately simple:

```text
Choose geography
      ↓
Choose Numbers or Percentages
      ↓
Read the same result in chart + table form
      ↓
Hover for denominator/context measures
      ↓
Use embedded guidance for interpretation
```

That simplicity is a strength. The upstream indicator methodology is substantial, while the Tableau layer keeps the reporting interaction controlled, consistent with the wider suite and easy to explain.
