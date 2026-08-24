# Last 6 Months of Life by Setting (MSG5) — Tableau Implementation

This page documents how the supplied MSG Indicator 5 aggregate output is presented in Tableau.

Compared with the Admissions Dashboard, this is a more compact implementation. The technical value is therefore in **clear parameter-driven presentation, coordinated chart/table behaviour, filtering, information design and accurate translation of a governed source indicator**, rather than in a large calculation layer.

## Dashboard architecture

The current evidence shows the dashboard combining:

- a stacked bar chart showing bed-day distribution by financial year;
- a detailed yearly table;
- a Council Area reporting filter;
- a **Bed Days** control for switching between Numbers and Percentages;
- dedicated navigation/help worksheets;
- an Information panel explaining the indicator.

The chart and table are designed to respond together so the user sees the same analytical state in both visual and tabular form.

## Bed Days control

The main reporting control is labelled **Bed Days** and has two states:

1. **Numbers**
2. **Percentages**

The supplied parameter definition will be documented in the [Parameters](parameters/README.md) section once its screenshot has been added.

At reporting level, the control changes the dashboard between:

### Numbers

Absolute bed-day values for:

- Community;
- Community Hospital;
- Large Hospital;
- Hospice / Specialist Palliative Care Unit.

### Percentages

The corresponding proportion of total possible six-month bed days in each setting.

This avoids duplicating the entire dashboard just to answer the two closely related questions:

```text
How many bed days were spent in each setting?
```

and

```text
What share of the final six months was spent in each setting?
```

## Numbers table

The **Bed Days by Setting** worksheet displays financial year down the rows and the four setting measures across columns.

In the Scotland-level example, 2024/25p displays approximately:

- Community: 9,467,029 bed days;
- Community Hospital: 166,842 bed days;
- Large Hospital: 945,892 bed days;
- Hospice / Specialist Palliative Care Unit: 45,571 bed days.

The displayed values are rounded for presentation while the source output retains half-day values where produced by the six-month methodology.

## Percentage table

The percentage version uses the same four categories and financial-year structure, but displays the distribution of possible bed days.

For Scotland in 2024/25p, the supplied source shows:

- Community: 89.1%;
- Community Hospital: 1.6%;
- Large Hospital: 8.9%;
- Hospice / Specialist Palliative Care Unit: 0.4%.

## Stacked bar chart

The stacked bar chart gives the same distribution a visual hierarchy, allowing year-to-year changes in the relative share of each care setting to be seen quickly.

The percentage version is especially useful for comparing composition across financial years because every bar represents the same 100% analytical denominator.

A matching Numbers version will be added to the evidence set once supplied.

## Council Area filter

The dashboard includes a Council Area control that changes the reporting geography while keeping the same chart/table structure.

The source data contains Council Area values as well as a Scotland aggregate. The public portfolio will use approved examples and will not deliberately surface granular combinations that could create disclosure concerns.

## Filter / display logic

The Tableau development screenshots show a calculated field named **BedDaysView_Filter** being used alongside the Bed Days control. The exact formula will be documented only after its calculation screenshot is supplied and reviewed.

The current implementation evidence also shows separate Number and Percentage worksheets. This suggests the dashboard switches which analytical worksheet is displayed according to the active Bed Days state rather than trying to force both formats into one visual.

That implementation choice will be confirmed from the remaining parameter/calculated-field screenshots before the case study is marked complete.

## Setting measures visible in Tableau

The current workbook evidence includes fields for:

- Community Bed days;
- Community/Hospital Bed days;
- Large Hospital Bed days;
- Palliative Bed days;
- Possible Bed days;
- Deaths;
- % Community;
- % Community/Hospital;
- % Large Hospital;
- % Palliative.

There is also a **KPI - Community** field visible in the workbook, which will be documented if it is part of the delivered dashboard behaviour.

## Worksheet composition

Observed analytical worksheets include:

- MSG - Bed Days by Setting;
- MSG - Bed Days by Setting %;
- MSG - Settings Breakdown (Bar) — Numbers;
- MSG - Settings Breakdown (Bar) — Percentages.

Shared interface worksheets include:

- Home;
- Go To;
- Help;
- Information.

The final inventory will be recorded in [Worksheets](worksheets/README.md) once the full worksheet screenshot set is available.

## Information panel

The Information panel explains the purpose and use of the dashboard rather than leaving the user to infer the indicator definition from the chart.

It covers:

- the final-six-month observation period;
- the four setting categories;
- Numbers versus Percentages;
- the financial-year structure;
- Council Area filtering;
- chart/table interpretation;
- the broad linked-data basis of the indicator;
- data-completeness and reporting caveats.

This is an important part of the BI design because the measure is conceptually more complex than a simple event count.

## Why this implementation is useful

The implementation is deliberately simple for the end user:

```text
Choose geography
      ↓
Choose Numbers or Percentages
      ↓
Read the same result in chart + table form
      ↓
Use embedded information for interpretation
```

That simplicity is a strength. The upstream indicator methodology is substantial, but the Tableau layer keeps the reporting interaction controlled and easy to explain.
