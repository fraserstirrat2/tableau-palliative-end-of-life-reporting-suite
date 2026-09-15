# Location of Death — Technical Case Study

This case study documents the **Location of Death** dashboard within the wider palliative and end-of-life care Tableau reporting suite.

> **Evidence status:** case-study framework created. A Scotland-level overview is already published in the parent `dashboards/` folder. Detailed implementation and validation evidence will be added after the live Tableau workbook is reviewed.

![Location of Death — Scotland-level overview](../01-LOD-Scotland-Level-Dashboard-Overview.png)

## Case study at a glance

| Employer question | Evidence to document |
| --- | --- |
| **What problem was being solved?** | Define the location-of-death reporting question, intended audience and analytical value. |
| **What was my role?** | Document direct Tableau/reporting contribution and separate shared/team ownership. |
| **What technical capability does it show?** | Capture the actual worksheets, measures, controls, calculations, navigation and information design. |
| **How were the numbers trusted?** | Record reconciliation, QA, refresh checks and any disclosure/validation steps. |
| **How did stakeholders influence the product?** | Add only retained examples of feedback and iterative change. |
| **Why does the solution matter?** | Explain what patterns/comparisons users can understand through the dashboard. |

## Reporting purpose

Document the measures, categories, reporting periods, geographies and intended users after reviewing the delivered dashboard. The final case study should preserve the terminology used in the actual reporting product.

## My contribution and ownership boundary

Describe the Tableau implementation, analytical/QA work and stakeholder-led changes personally contributed. Clearly attribute shared/team-owned data preparation and production logic.

## Dataset and analytical context

Document the Tableau-ready source, reporting grain, categories/measures, time/geography coverage, definitions/caveats and whether logic is supplied upstream or calculated in Tableau.

## Tableau interaction design

Capture the real controls, filters, parameters and dashboard actions. Explain how they support meaningful comparison without overstating the technical complexity.

## Dashboard composition

Identify the analytical worksheets and suite-wide interface components after workbook review. See [Worksheets](worksheets/README.md).

## Information design

Record how location categories, definitions, caveats, labels, help text and navigation reduce ambiguity for users.

## Validation approach

Use a clear evidence chain:

```text
Governed source / prepared output
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

Use approved **Scotland-level aggregated evidence only**. Do not publish granular/patient-level information, Tableau workbook/extract files, restricted code, credentials, internal URLs or unauthorised organisational material.

## Next evidence required

1. Main Scotland-level dashboard screenshot(s).
2. Information/help panel.
3. Worksheet inventory.
4. Filters/parameters/actions.
5. Relevant calculated fields.
6. Source/methodology and QA notes.
7. Evidence-backed stakeholder-development examples.

Once supplied, rewrite this framework into a finished employer-facing case study.