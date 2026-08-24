# Last 6 Months of Life by Setting (MSG5) — Validation and Development

This page documents the validation approach and development history for the Tableau reporting layer built from the supplied MSG Indicator 5 aggregate output.

Unlike the Admissions Dashboard, the upstream MSG5 production pipeline is maintained by another PHS team. Validation for this case study therefore focuses on demonstrating that the **supplied indicator output has been translated into Tableau accurately and consistently**.

## Validation principle

The key question is straightforward:

> Does the Tableau dashboard reproduce the supplied MSG5 values correctly across years, settings, geography selections and display modes?

The main evidence chain is:

```text
Supplied MSG5 aggregate output
        ↓
Tableau data source
        ↓
Numbers worksheets
        ↓
Percentage worksheets
        ↓
Stacked chart + table
        ↓
Dashboard controls and information guidance
```

## Source reconciliation

The supplied CSV contains five financial years from 2020/21 to 2024/25p and the same four setting measures used in the dashboard.

For Scotland, source values can be compared directly with the Tableau view. For example, 2024/25p contains approximately:

| Setting | Source value |
| --- | ---: |
| Community | 9,467,028.5 bed days |
| Community Hospital | 166,841.5 bed days |
| Large Hospital | 945,892.0 bed days |
| Hospice / Palliative | 45,570.5 bed days |
| Possible bed days | 10,625,332.5 |
| Deaths | 58,221 |

The Tableau Numbers table displays these values rounded to whole bed days for presentation.

## Percentage checks

The supplied source also contains the percentage distribution for each setting. The reporting-layer checks should confirm that:

- Tableau displays the correct percentage field for each setting;
- the active financial-year values match the source;
- the four displayed percentages sum to approximately 100%;
- minor differences caused by display rounding are understood rather than treated as data-quality failures.

For Scotland in 2024/25p, the displayed distribution is approximately:

```text
89.1% Community
 1.6% Community Hospital
 8.9% Large Hospital
 0.4% Hospice / Palliative Care Unit
-----
100.0%
```

## Numbers / Percentages selector testing

The Bed Days control should be tested in both states:

- **Numbers**
- **Percentages**

For each state, checks should confirm:

- the correct bar worksheet is visible;
- the correct table worksheet is visible;
- legends and labels remain appropriate;
- the chart and table refer to the same financial years and geography;
- switching the control does not leave stale values or mismatched formatting.

The exact `BedDaysView_Filter` logic will be added after the calculated-field screenshot is reviewed.

## Geography filter testing

The Council Area filter should be checked to ensure that:

- the selected area updates both chart and table;
- the active display mode remains unchanged when geography changes;
- the correct source row is returned for the selected year and area;
- Scotland returns the national aggregate row supplied in the dataset.

Public evidence will remain within the approved portfolio boundary.

## Chart / table alignment

Because the dashboard intentionally presents the same indicator in two forms, a key QA check is that the stacked bar and detailed table stay aligned.

This includes:

- financial-year order;
- setting names;
- setting colours/legend mapping;
- active Numbers or Percentages mode;
- geography selection;
- source values.

This reduces the risk of a user reading one value in the table while the chart is showing a different analytical state.

## Methodology consistency checks

The upstream source methodology provides additional reasonableness checks for the supplied aggregate data:

```text
Possible bed days = 182.5 × deaths
```

and:

```text
Community + Community Hospital + Large Hospital + Palliative
= Possible bed days
```

subject to the source calculation precision.

These relationships provide useful analytical checks when validating a refreshed file before or during Tableau updates.

## Development review

This dashboard forms part of the wider palliative and end-of-life Tableau reporting suite and is reviewed within the same iterative team environment.

For this specific MSG5 case study, development-history claims will be added only where the retained project notes support them. The repository will not invent a large change history for a relatively straightforward dashboard simply to make the case study appear more complex.

Evidence still to capture includes:

- any documented stakeholder requests specific to MSG5;
- changes to terminology or labels;
- changes to the Bed Days selector or chart/table design;
- information-panel refinements;
- any source-file or refresh issues identified during development;
- any final QA/sign-off notes relevant to the dashboard.

## Information and interpretation review

The Information panel is part of the validation approach because correct use depends on understanding the indicator.

Review should confirm that users are told:

- the analysis covers the final six months of life;
- the four setting categories are clearly described;
- Numbers and Percentages represent different views of the same source indicator;
- the Council Area control changes reporting geography;
- service configuration may affect comparisons between areas;
- the indicator is based on linked hospital/death information and can be affected by source completeness/reporting differences.

## Governance boundary

The public repository does not need the supplied source CSV or upstream production code to demonstrate that this Tableau layer was validated.

The evidence will instead consist of:

- approved dashboard screenshots;
- worksheet screenshots;
- parameter/calculated-field evidence;
- source-to-dashboard reconciliation notes;
- high-level methodology attribution;
- documented development decisions where available.

## Definition of done for this case study

MSG5 can be marked complete when a reviewer can answer **yes** to the following:

- Can I understand what the indicator measures?
- Can I see clearly what work was upstream team-owned versus Tableau work completed here?
- Can I see how Numbers and Percentages are implemented?
- Can I trace displayed values back to the supplied source output?
- Can I understand the worksheet/control structure?
- Can I see the interpretation and governance safeguards?
- Can I understand why the dashboard is useful without needing access to the managed Tableau environment?
