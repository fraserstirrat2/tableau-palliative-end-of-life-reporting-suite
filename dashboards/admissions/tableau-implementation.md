# Admissions Dashboard — Tableau Implementation

This page documents how the Admissions Dashboard is implemented in Tableau and how the individual controls, calculations and worksheets work together as one reusable reporting interface.

## Dashboard architecture

The dashboard combines:

- analytical worksheets;
- parameter-driven calculations;
- user filters;
- Scotland comparator logic;
- navigation worksheets;
- information/help design;
- a yearly summary table.

The main design objective was to avoid building a separate dashboard for every time period or analytical measure. Instead, reusable Tableau logic allows the same visual structure to respond dynamically to the user's selections.

## Core user controls

Two parameters sit at the centre of the design.

### Time Window

The **Time Window** parameter allows the user to switch between:

- 7 Days
- 14 Days
- 3 Months
- 6 Months
- 12 Months

The parameter feeds reusable calculated fields for admissions, patients, bed days and deaths. For example, **Selected Admissions** checks the Time Window value and returns the matching upstream field for that period. The same design is used for Selected Deaths and the other activity measures.

This gives the dashboard one consistent calculation layer even though the analytical dataset contains separate period-specific measures.

See the [parameter evidence](parameters/README.md) and [selected activity calculations](calculated-fields/selected-activity-measures/README.md).

### Trend Selector

The **Trend Selector** switches the main trend chart between:

- Admissions Per Death
- Average Length of Stay

The user can therefore change the analytical question without leaving the dashboard or duplicating the full worksheet layout.

## Admissions per Death

The Tableau calculation uses the selected activity measures rather than a fixed source field.

Conceptually:

```text
Admissions per Death
=
Selected Admissions / Selected Deaths
```

A zero-denominator check returns null when Selected Deaths is zero. This prevents invalid division and ensures the measure always follows the currently selected Time Window.

This calculated-field design is evidenced in the [Core Measures](calculated-fields/core-measures/README.md) folder.

## Filter design

The dashboard includes filters for analytical dimensions including:

- Health Board;
- HSCP / local-area geography;
- Age Group;
- Sex;
- Admission Type;
- Cause of Death;
- SIMD;
- Urban/Rural classification;
- Location / care-setting classification.

For the public portfolio, screenshots are restricted to approved Scotland-level views. The production reporting environment can support more granular controlled analysis, but those views are not reproduced here.

## Cause-of-death filter behaviour

The cause-of-death filter requires deliberate user guidance because the dataset contains both detailed cause groups and an aggregated **Non-cancer** category.

**Cancers** is one mutually distinct category. **Non-cancer**, however, is an aggregate of all the remaining cause groups. Selecting Non-cancer together with one of its component non-cancer categories would therefore count that activity twice in additive measures.

The dashboard includes an explicit on-screen warning telling users to:

- use **Cancers + Non-cancer** when they need the complete cancer/non-cancer split;
- avoid selecting **Non-cancer** together with another individual non-cancer cause group.

This is an example of information design being used as part of data-quality control rather than relying on users to infer the structure of the analytical dataset.

## Scotland comparator logic

The trend view retains a Scotland-level comparator alongside the selected analytical result. Dedicated Level of Detail calculations support the national admissions, patients, bed days and deaths measures and the derived Scotland comparator values.

The purpose is to provide context around the selected trend rather than presenting a result in isolation.

See [Scotland Comparator Logic](calculated-fields/scotland-comparator-logic/README.md).

## Worksheet composition

The final dashboard is assembled from seven supplied Tableau worksheets.

### Analytical worksheets

- Admissions Per Death trend chart
- Average Length of Stay trend chart
- Summary table

### Interface worksheets

- Home icon
- Help icon
- Information icon
- Go-To icon

Using separate interface worksheets allows navigation and help functions to remain part of the workbook design while keeping the analytical worksheets focused on reporting logic.

See [Worksheets](worksheets/README.md).

## Information design

The information panel explains:

- what the dashboard measures;
- the available analytical periods;
- the data sources at a high level;
- how the charts and table should be interpreted;
- how to use the filters and parameters;
- important methodological caveats, including the cause-of-death selection rule.

This supports self-service use and reduces the risk of a user applying a technically valid Tableau selection that would produce an analytically misleading result.

## Screenshot evidence

The public evidence set contains ten approved Scotland-level dashboard states. Together they demonstrate:

- all five Time Window selections;
- both Trend Selector measures;
- different approved demographic and analytical filter combinations;
- dynamic updates to the chart and summary table.

The main case study uses only a small number of these images, while the full evidence set is available in [Dashboard Screenshots](dashboard-screenshots/README.md).

## Why this implementation is useful

The technical value of the dashboard is not simply the chart type. The reusable architecture turns a multi-period analytical output into a single controlled reporting interface:

```text
Time Window parameter
        ↓
Selected activity measures
        ↓
Derived calculations
        ↓
Trend Selector
        ↓
Dynamic trend + comparator + summary table
```

That structure makes the workbook easier to extend, validate and explain than maintaining separate dashboard pages for every combination of time period and measure.
