# Admissions Dashboard — Validation and Development

This page records how the Admissions Dashboard was reviewed, tested and refined over multiple development cycles. The purpose is to show the work as an evolving BI product rather than a one-off visualisation.

## Iterative development approach

Development has been supported through **fortnightly Palliative and End-of-Life Care review meetings**. These sessions provide a recurring forum to discuss analytical outputs, information requests, refreshes, data completeness, workload, dashboard demonstrations, upcoming releases and potential reporting improvements.

Dashboard changes were therefore not developed in isolation. Feedback from analysts and wider stakeholders was translated into Tableau changes and, where required, into updates to the upstream analytical output.

The case study deliberately separates **team-based analytical development** from the Tableau work I can evidence directly. It does not present shared R development or colleagues' contributions as solely my own work.

## Development timeline

| Period | Examples of development activity |
| --- | --- |
| **February 2026** | Initial dashboard review and build-out; assessment of relevant worksheets and outputs; early work on filter behaviour and dashboard layout. |
| **March 2026** | Refinement of Admissions controls, including multi-selection behaviour, legend presentation, information guidance and the move toward **Admissions per Death** as the primary trend measure rather than a less clearly defined rate label. |
| **April 2026** | Further terminology and usability work, including bed-day wording, Health Board presentation, tooltip review and strengthening information-panel content. |
| **May 2026** | Numerical checks against established Admissions outputs, review of the latest analysis and a clinical stakeholder demonstration. A request for an additional **7-day** pre-death view was taken forward into the analytical pipeline and Tableau Time Window control. |
| **Ongoing** | Fortnightly review, repeated calculation checks, filter/parameter testing, information-design refinement, dashboard navigation checks and validation of refreshed analytical outputs in the controlled Tableau development environment. |

The 7-day enhancement is a particularly useful example of stakeholder-led iteration: the reporting architecture was flexible enough to add a new analytical period without requiring an entirely separate dashboard.

## Numerical validation

The Tableau dashboard has been validated against established analytical outputs rather than checked only by visual inspection.

For the established **14-day, 3-month, 6-month and 12-month** periods, numerical checks were carried out against the corresponding annual **Number of Admissions** publication outputs. These outputs use the same underlying analytical concepts and provide a practical benchmark for confirming that the refreshed code and Tableau results reconcile as expected.

The later **7-day** view was introduced as an enhancement after stakeholder feedback. Because it was a new analytical window rather than one of the pre-existing publication outputs, it was checked against the prepared analytical dataset and the same reusable Tableau calculation logic rather than presented as though an existing 7-day publication benchmark already existed.

Validation checks included:

- reconciling Tableau totals with the prepared analytical outputs;
- comparing established periods with the corresponding annual Admissions publication figures;
- confirming admissions, patients, bed days and deaths align with the selected Time Window;
- independently checking **Admissions per Death = Selected Admissions / Selected Deaths**;
- independently checking **Average Length of Stay = Selected Beddays / Selected Patients**;
- confirming divide-by-zero handling returns null where the denominator is zero;
- testing the Scotland comparator against the national result;
- checking multiple financial years and approved filter combinations;
- confirming the summary table and trend chart remain aligned after parameter changes.

The current Admissions reporting includes **final 2024/25 data**. This status is now reflected in the portfolio case study so the repository does not describe the latest year as provisional.

This matters because the workbook contains reusable logic: one successful dashboard state is not enough to demonstrate that the calculations behave correctly across all five periods and both derived trend measures.

## Parameter and filter testing

The two main parameters were tested across their available values:

- **Time Window:** 7 Days, 14 Days, 3 Months, 6 Months and 12 Months;
- **Trend Selector:** Admissions Per Death and Average Length of Stay.

Filter testing also covered demographic, admission, geography, deprivation, rurality, location and cause-of-death selections.

The public screenshot set intentionally captures different approved Scotland-level filter states so the repository demonstrates that the workbook responds to more than its default view.

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

## Evidence retained

The Admissions case study contains:

- **10 dashboard screenshots** across all five analytical windows and both trend measures;
- **7 Tableau worksheets**;
- **2 parameters**;
- **19 calculated fields** grouped by analytical purpose;
- a documented development timeline based on retained working notes;
- methodology and validation documentation explaining how the dashboard was checked without publishing restricted source material.

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

The strongest evidence from the project is the combination of **technical implementation + QA + iteration + stakeholder review**. The dashboard changed in response to numerical checks, analyst review and stakeholder feedback, while the calculation and parameter architecture allowed those changes to be incorporated into the same reporting product.
