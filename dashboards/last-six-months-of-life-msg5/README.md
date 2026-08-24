# Last 6 Months of Life by Setting (MSG5) — Technical Case Study

This case study documents the Tableau implementation of the **Last 6 Months of Life by Setting** dashboard within the wider palliative and end-of-life care reporting suite.

The dashboard is based on **MSG Indicator 5 — End of Life** analytical output supplied by another Public Health Scotland team. I did **not** develop or run the upstream MSG production code. My role in this portfolio evidence is therefore described accurately: I worked with the supplied aggregated indicator output and developed the Tableau reporting layer used to present, filter and explain it.

> **Evidence status:** case-study structure created. Dashboard, worksheet, parameter and calculated-field evidence will be added after the remaining screenshots have been reviewed.

## Case study at a glance

| Employer question | Evidence from this dashboard |
| --- | --- |
| **What problem was being solved?** | A multi-setting end-of-life indicator needed to be presented in a clear interactive format so users could compare how bed days were distributed across Community, Community Hospital, Large Hospital and Hospice / Specialist Palliative Care settings over time. |
| **What was my role?** | I used the supplied MSG5 aggregated output as the Tableau data source and developed the reporting layer: dashboard layout, numbers/percentage switching, Council Area filtering, worksheet composition, navigation and information design, plus validation of the displayed values against the supplied source output. |
| **What technical capability does it show?** | Tableau parameter/control design, switching between absolute and percentage views, stacked-bar composition, tabular detail, calculated-field/filter logic, geography filtering, reusable navigation and information/help design. |
| **How were the numbers trusted?** | Tableau values can be reconciled directly to the supplied MSG Indicator 5 output. The upstream analytical methodology derives a fixed six-month observation window and allocates bed days across care settings before the aggregated dataset reaches Tableau. |
| **How did stakeholders influence the product?** | This dashboard sits within the same reporting-suite development cycle as the other palliative and end-of-life dashboards, with iterative review of presentation, controls, terminology and explanatory guidance. Specific MSG5 development examples will be added only where retained evidence supports them. |
| **Why does the solution matter?** | It converts a detailed indicator table into an accessible longitudinal view, while allowing users to move between total bed-day volumes and percentage distributions without maintaining separate dashboard pages. |

## Reporting purpose

The dashboard presents the **last six months of life by care setting**, showing how time is distributed across four reporting categories:

- **Community**
- **Community Hospital**
- **Large Hospital**
- **Hospice / Specialist Palliative Care Unit**

The supplied Tableau dataset contains financial-year results from **2020/21 to 2024/25p** across Council Area reporting geographies and a Scotland aggregate.

The dashboard combines a stacked bar chart with a detailed table so the same result can be read visually and numerically.

## My contribution and ownership boundary

The upstream MSG Indicator 5 analytical code was supplied and maintained by another PHS team. The source scripts show that the production methodology combines linked hospital and death-record data, applies the six-month end-of-life methodology, derives setting-level bed days and produces aggregated indicator outputs.

I did not author or run that production pipeline and will not present it as my own work.

My contribution is the **Tableau reporting implementation built on the supplied aggregated output**, including:

- connecting the prepared MSG5 dataset to the Tableau workbook;
- designing the dashboard layout and visual hierarchy;
- implementing the **Bed Days** view control;
- presenting both **Numbers** and **Percentages** through the same dashboard;
- applying the Council Area reporting filter;
- composing the stacked bar and summary table worksheets;
- integrating Home, Go To, Help and Information navigation components;
- documenting how the indicator should be interpreted;
- checking that Tableau values reconcile to the supplied MSG5 data.

This boundary is important because the portfolio should demonstrate professional BI delivery without claiming ownership of shared analytical pipelines.

## Dataset used by Tableau

The supplied Tableau-ready CSV contains **170 aggregated rows and 12 fields**:

- Financial Year
- Council Area
- Community Bed days
- Palliative Bed days
- Community/Hospital Bed days
- Large Hospital Bed days
- Possible Bed days
- % Community
- % Palliative
- % Community/Hospital
- % Large Hospital
- Deaths

The current extract covers **five financial years** and **34 reporting geography values**, including Scotland and the combined Stirling and Clackmannanshire reporting area.

The dataset itself is not published in this repository. The case study documents its structure and Tableau use without distributing the underlying management-information file.

## Indicator methodology at a glance

The supplied upstream methodology defines the final six months of life as a **183-day period**, with an exact six-month maximum represented as **182.5 bed days per death** in the final calculations.

Hospital activity is classified into setting categories before aggregation. The analytical output then calculates:

```text
Possible bed days = 182.5 × deaths
```

and derives Community bed days as the remaining time after the identified inpatient/hospice settings are removed:

```text
Community bed days = Possible bed days
                   - Large Hospital bed days
                   - Community Hospital bed days
                   - Hospice / Palliative Care Unit bed days
```

The four percentage measures are then calculated as each setting's bed days divided by Possible bed days.

A fuller explanation is available in [Data Pipeline and Methodology](data-pipeline-and-methodology.md).

## Tableau interaction design

### Bed Days view selector

The dashboard contains a **Bed Days** control with two states:

1. **Numbers**
2. **Percentages**

This allows the same analytical story to be viewed from two perspectives:

- absolute bed-day volume; or
- proportional distribution of the six-month period.

The stacked bar and detailed table update together so the displayed chart and numeric values remain aligned.

### Council Area filter

A Council Area control allows the dashboard to move between the national result and individual reporting areas in the controlled workbook.

For the public portfolio, screenshots will remain within the approved reporting boundary and will be selected for analytical value rather than to expose granular small-number combinations.

## Dashboard composition

The current evidence shows the dashboard being assembled from a small set of focused Tableau components:

- **Bed Days by Setting — Numbers table**
- **Bed Days by Setting — Percentages table**
- **Settings Breakdown — Numbers stacked bar**
- **Settings Breakdown — Percentages stacked bar**
- Home navigation
- Go To navigation
- Help
- Information

The exact worksheet inventory will be finalised after all screenshots are supplied and reviewed.

See [Worksheets](worksheets/README.md).

## Information design

The Information panel explains:

- what the dashboard presents;
- the four care settings;
- the ability to switch between values and percentage distributions;
- the financial-year structure;
- the Council Area control;
- how to read the stacked bar and detail table;
- the broad linked hospital/death-record basis of the indicator;
- interpretation caveats around data completeness and differences in service configuration.

This is important because a percentage such as **89.1% Community** is meaningful only when the user understands what the denominator and care-setting categories represent.

## Example Scotland-level result

In the supplied 2024/25p Scotland view, the dashboard shows approximately:

- **89.1% Community**
- **1.6% Community Hospital**
- **8.9% Large Hospital**
- **0.4% Hospice / Specialist Palliative Care Unit**

The case study uses these values as evidence of the display logic, not as a causal interpretation of why care patterns differ between years or areas.

## Validation approach

Because this Tableau dashboard uses a supplied aggregated indicator dataset, the key reporting-layer validation is direct reconciliation between:

```text
Supplied MSG5 output
        ↓
Tableau source fields / calculations
        ↓
Numbers view
        ↓
Percentage view
        ↓
Stacked bar + table alignment
```

Validation evidence will document:

- source-row reconciliation for selected financial years;
- totals and percentage checks;
- confirmation that percentages sum to approximately 100%, allowing for rounding;
- Council Area filter behaviour;
- Bed Days selector behaviour;
- agreement between the chart and tabular display;
- navigation and information-panel behaviour.

See [Validation and Development](validation-and-development.md).

## Evidence structure

This case study will be organised into:

- [Dashboard screenshots](dashboard-screenshots/README.md)
- [Worksheets](worksheets/README.md)
- [Parameters](parameters/README.md)
- [Calculated fields](calculated-fields/README.md)
- [Data pipeline and methodology](data-pipeline-and-methodology.md)
- [Tableau implementation](tableau-implementation.md)
- [Validation and development](validation-and-development.md)

Unlike the Admissions Dashboard, MSG5 is a comparatively compact reporting product. The documentation will therefore stay proportionate: enough evidence to show the logic clearly without creating artificial complexity where the implementation is straightforward.

## Governance and portfolio boundary

The repository will not publish:

- the supplied MSG5 CSV;
- the production R scripts supplied by another team;
- linked record-level data;
- credentials, internal paths or infrastructure details;
- granular screenshots outside the approved portfolio boundary.

The public case study will focus on **Tableau implementation, analytical interpretation, validation, information design and appropriate attribution of upstream methodology**.
