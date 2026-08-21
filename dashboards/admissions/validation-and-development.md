# Admissions Dashboard — Validation and Development

This page records how the Admissions Dashboard was reviewed, tested and refined over multiple development cycles. The purpose is to show the work as an evolving BI product rather than a one-off visualisation.

## Iterative development approach

Development was supported through recurring palliative and end-of-life care review meetings where analytical outputs, refreshes, data-quality issues, reporting requirements and dashboard changes could be discussed. Feedback was then translated into changes to the Tableau workbook and, where necessary, the upstream analytical output.

The case study deliberately separates **team-based analytical development** from the Tableau work I can evidence directly. It does not present shared R development or colleagues' contributions as solely my own work.

## Development timeline

| Period | Examples of development activity |
| --- | --- |
| **February 2026** | Initial dashboard review and build-out; assessment of relevant worksheets and outputs; early work on filter behaviour and dashboard layout. |
| **March 2026** | Refinement of Admissions controls, including multi-selection behaviour, legend presentation, information guidance and the move toward **Admissions per Death** as the primary trend measure rather than a less clearly defined rate label. |
| **April 2026** | Further terminology and usability work, including bed-day wording, Health Board presentation, tooltip review and strengthening information-panel content. |
| **May 2026** | Numerical checks against analytical outputs, review of the latest Admissions analysis and clinical stakeholder demonstration. A request for an additional **7-day** pre-death view was taken forward into the analytical pipeline and Tableau Time Window control. |
| **Ongoing** | Repeated checks of calculations, filters, parameters, information guidance, dashboard navigation and refreshed analytical outputs in the controlled Tableau development environment. |

The 7-day enhancement is a particularly useful example of stakeholder-led iteration: the reporting architecture was flexible enough to add a new analytical period without requiring an entirely separate dashboard.

## Numerical validation

The dashboard has been checked against the prepared analytical outputs rather than validated only by visual inspection.

Checks include:

- comparing Tableau totals with the upstream analytical outputs;
- confirming admissions, patients, bed days and deaths align with the selected Time Window;
- checking Admissions per Death against the underlying selected admissions and death counts;
- testing the Scotland comparator against the national result;
- checking multiple financial years and filter combinations;
- confirming the summary table and trend chart remain aligned after parameter changes.

This matters because the workbook contains reusable logic: one successful dashboard state is not enough to prove that the calculations behave correctly across all five periods.

## Parameter and filter testing

The two main parameters were tested across their available values:

- **Time Window:** 7 Days, 14 Days, 3 Months, 6 Months and 12 Months;
- **Trend Selector:** Admissions Per Death and Average Length of Stay.

Filter testing also covered demographic, admission, geography, deprivation, rurality, location and cause-of-death selections.

The public screenshot set intentionally captures different Scotland-level filter states so the repository demonstrates that the workbook responds to more than its default view.

## Cause-of-death validation and user guidance

The analytical dataset contains detailed cause-of-death categories plus an aggregate **Non-cancer** category. Because Non-cancer is formed from the detailed non-cancer groups, selecting it together with one of those component categories would double count the same activity in additive measures.

The dashboard therefore includes visible instructions telling users not to combine Non-cancer with another non-cancer cause group. **Cancers + Non-cancer** can be used together because those two categories form the intended complete split.

Documenting this rule in the dashboard is part of validation and governance: correct totals depend not only on technically working filters, but also on users understanding which selections are analytically compatible.

## Information and usability review

Development notes show repeated attention to the reporting experience, including:

- naming and terminology;
- tooltip clarity;
- information-panel content;
- filter labels and selection behaviour;
- chart legends;
- table presentation;
- navigation controls;
- removing unnecessary or confusing elements.

The information icon therefore represents part of the final quality-control approach, not simply decorative help text. It records definitions and caveats at the point where users interact with the analysis.

## Technical evidence retained

The Admissions case study contains:

- **10 dashboard screenshots** across all five analytical windows and both trend measures;
- **7 Tableau worksheets**;
- **2 parameters**;
- **19 calculated fields** grouped by analytical purpose.

These artefacts allow a technical reviewer to inspect the implementation without requiring access to the managed Tableau environment.

## Deployment status

The workbook is being developed and validated within a controlled Tableau pre-production environment as part of the wider reporting-suite development process. The public portfolio does not present the workbook as an unrestricted public data release.

## Governance boundary

The public case study does not include:

- patient-level or otherwise granular source data;
- operational R code used to access linked datasets;
- internal file-system or credential information;
- local-level screenshots that could expose small-number management information.

The portfolio evidence instead focuses on approved Scotland-level examples, analytical methodology, reusable Tableau implementation and the documented review process.

## What this development history demonstrates

The strongest evidence from the project is the combination of **technical implementation + QA + iteration**. The dashboard changed in response to numerical checks, analyst review and stakeholder feedback, while the calculation and parameter architecture allowed those changes to be incorporated into the same reporting product.
