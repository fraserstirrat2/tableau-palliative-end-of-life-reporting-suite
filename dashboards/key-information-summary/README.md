# Key Information Summary — Technical Case Study

This case study documents the **Key Information Summary (KIS)** dashboard within the wider palliative and end-of-life care Tableau reporting suite.

> **Evidence status:** case-study framework created. The Scotland-level overview is already published in the parent `dashboards/` folder. The detailed worksheet, parameter, calculated-field, methodology and validation evidence will be added only after the corresponding Tableau evidence has been reviewed.

![Key Information Summary — Scotland-level overview](../01-KIS-Scotland-Level-Dashboard-Overview.png)

## Case study at a glance

| Employer question | Evidence to document |
| --- | --- |
| **What problem was being solved?** | Confirm the reporting question, intended users and why a summary view was needed. |
| **What was my role?** | Document the Tableau/reporting work completed directly, while separating shared team or upstream analytical work. |
| **What technical capability does it show?** | Capture the real worksheets, controls, calculations, filters, navigation and information design used by this dashboard. |
| **How were the numbers trusted?** | Record the source-to-Tableau validation, refresh/QA checks and any reconciliation performed. |
| **How did stakeholders influence the product?** | Add only retained examples of feedback, iteration, terminology, layout or interaction changes. |
| **Why does the solution matter?** | Explain what users can understand or decide more easily from the summary view. |

## Reporting purpose

This section will explain what the KIS dashboard presents, who it supports and how it fits into the wider reporting suite. The final wording should be based on the live dashboard and retained project evidence rather than assumptions.

## My contribution and ownership boundary

Document the parts personally developed, maintained, validated or improved in Tableau. Where data preparation, analytical logic or production processes are shared/team-owned, describe them accurately without claiming sole ownership.

## Dataset and analytical context

Document:

- the Tableau-ready source used by the dashboard;
- the reporting period and geography coverage;
- the main measures exposed to users;
- any important definitions or caveats;
- which logic is source-supplied versus created in Tableau.

Do not publish underlying restricted datasets, operational code or internal file paths.

## Tableau interaction design

Capture only the controls that genuinely drive the delivered dashboard, for example filters, parameters, navigation actions or display selectors. Do not create artificial complexity simply to mirror the Admissions Dashboard.

## Dashboard composition

The final evidence should identify the analytical worksheets and shared interface components that assemble the KIS dashboard. See [Worksheets](worksheets/README.md).

## Information design

Record how definitions, help text, caveats, labels and navigation support correct interpretation by technical and non-technical users.

## Validation approach

Validation should show a clear evidence chain:

```text
Prepared / governed source output
        ↓
Tableau data source
        ↓
Worksheets and calculations
        ↓
Dashboard controls and visual state
        ↓
Displayed Scotland-level result
```

See [Validation and Development](validation-and-development.md).

## Evidence structure

- [Dashboard screenshots](dashboard-screenshots/README.md)
- [Worksheets](worksheets/README.md)
- [Parameters](parameters/README.md)
- [Calculated fields](calculated-fields/README.md)
- [Data pipeline and methodology](data-pipeline-and-methodology.md)
- [Tableau implementation](tableau-implementation.md)
- [Validation and development](validation-and-development.md)

## Governance and portfolio boundary

The public case study should use approved **Scotland-level aggregated evidence only**. Do not publish patient-level or granular data, Tableau workbooks/extracts, restricted code, credentials, internal URLs or organisational files that are not approved for public use.

## Next evidence required

1. Main Scotland-level dashboard screenshot(s).
2. Information/help panel.
3. Full worksheet inventory relevant to KIS.
4. Parameter/filter/control definitions.
5. Calculated fields that genuinely contribute to the dashboard.
6. Source/methodology notes and QA evidence.
7. Any retained stakeholder-development examples.

Once supplied, this framework should be rewritten into a finished employer-facing case study rather than left as a checklist.