# Admissions Dashboard — Tableau Implementation

This page documents how the Admissions Dashboard is implemented in Tableau and how its interactive components work together.

## Dashboard architecture

The dashboard combines analytical worksheets, parameters, calculated fields, filters, navigation components and information design into one reporting interface.

### Core user controls

Two parameters drive key analytical behaviour:

- **Time Window** — 7 Days, 14 Days, 3 Months, 6 Months or 12 Months.
- **Trend Selector** — switches the primary trend between Admissions Per Death and Average Length of Stay.

These controls work alongside filters for broader demographic, admission, cause-of-death and geographic selections.

## Calculation architecture

The calculated-field evidence is organised into logical families:

1. **Core analytical measures** — Admissions per Death and Average Length of Stay.
2. **Selected activity measures** — parameter-controlled admissions, bed days, deaths and patients.
3. **Time-window row logic** — row-level calculations supporting the selected analytical period.
4. **Scotland comparator logic** — national comparator measures retained alongside the selected view.
5. **Trend-selection logic** — calculations used to control which measure is plotted.
6. **Change analysis** — year-on-year calculations used for additional analytical context.

See [Calculated Fields](calculated-fields/README.md) for the complete evidence index.

## Worksheet composition

The final dashboard is assembled from analytical worksheets and dedicated interface components. The analytical worksheets include the trend charts and summary table; separate worksheets provide navigation and information controls.

See [Worksheets](worksheets/README.md) for the full set.

## Information design

The dashboard includes an information panel that explains the data presented, chart interpretation, dashboard controls and important methodological notes. This is part of the reporting design rather than an afterthought: the aim is to support correct interpretation and self-service use.

## Portfolio evidence

The public case study includes all approved Scotland-level dashboard examples supplied for the portfolio. The screenshots deliberately demonstrate multiple time windows, filter states and both trend-selector outcomes so the interactive behaviour can be assessed without access to the production workbook.
