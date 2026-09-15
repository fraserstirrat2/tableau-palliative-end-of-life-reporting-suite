# Service Utilisation — Technical Case Study

This case study documents the **Service Utilisation** dashboard within the wider palliative and end-of-life care Tableau reporting suite.

> **Evidence status:** case-study framework created. A Scotland-level overview is already published in the parent `dashboards/` folder. Detailed technical evidence will be added after the live Tableau implementation is reviewed.

![Service Utilisation — Scotland-level overview](../01-Service-Utilisation-Scotland-Level-Dashboard-Overview.png)

## Case study at a glance

| Employer question | Evidence to document |
| --- | --- |
| **What problem was being solved?** | Define the service-use reporting question and intended users. |
| **What was my role?** | Record the Tableau/reporting work completed directly and separate wider team ownership. |
| **What technical capability does it show?** | Capture the real worksheets, filters, parameters, calculations, navigation and interaction design. |
| **How were the numbers trusted?** | Document reconciliation, QA, refresh checks and source-to-dashboard validation. |
| **How did stakeholders influence the product?** | Add evidence-backed examples of iterative changes only. |
| **Why does the solution matter?** | Explain what service-use patterns the interactive reporting helps users understand. |

## Reporting purpose

Document the analytical question, measures, reporting periods, users and how Service Utilisation fits into the wider suite. Avoid making claims until the dashboard evidence is reviewed.

## My contribution and ownership boundary

Describe only the Tableau, analytical, QA or supporting workflow elements personally delivered. Clearly distinguish shared/team-owned data preparation, code and production processes.

## Dataset and analytical context

Document the Tableau-ready source, grain, reporting coverage, main measures, definitions/caveats and whether each important measure is supplied upstream or calculated in Tableau.

## Tableau interaction design

Capture the actual user controls and how they change the analytical state. The goal is to explain the real implementation, not to force the dashboard into the same technical complexity as Admissions.

## Dashboard composition

Identify the analytical worksheets and shared interface components after reviewing the workbook. See [Worksheets](worksheets/README.md).

## Information design

Record how labels, definitions, caveats, help text and navigation support correct interpretation of service-use measures.

## Validation approach

Use a traceable chain:

```text
Governed source / prepared reporting output
        ↓
Tableau source and calculations
        ↓
Worksheets
        ↓
Filters / parameters / actions
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

Use approved **Scotland-level aggregated evidence only**. Do not publish patient-level or granular data, workbooks/extracts, operational code, credentials, internal URLs or restricted organisational material.

## Next evidence required

1. Main Scotland-level dashboard screenshot(s).
2. Information/help panel.
3. Relevant worksheet inventory.
4. Filters/parameters and their real configurations.
5. Calculated fields that drive delivered behaviour.
6. Source/methodology and validation notes.
7. Evidence-backed stakeholder/development examples.

Once supplied, rewrite this framework into a finished case study.