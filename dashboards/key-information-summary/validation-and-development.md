# Key Information Summary — Validation and Development

This page documents how the **Key Information Summary (KIS)** dashboard was checked and how it evolved from two separate Tableau products into one combined reporting solution.

The main validation question was:

> Can one combined KIS source and one Tableau dashboard reproduce the established Accesses and Patients reporting states without losing valid source-only records or inflating measures through duplicate joins?

## Development timeline

### 1. Separate Accesses and Patients dashboards

KIS Accesses and KIS Patients were first developed as separate Tableau views. Early work focused on consistent naming, Financial Year controls, NHS Health Board labels, Practice terminology, KIS capitalisation, legend/table formatting and relevant-value behaviour for lower-level filters.

Those separate dashboards later became useful QA references when the combined design was introduced.

### 2. Source totals-row issue identified

During Patients development, an unexpected `NA` pattern was traced back to an extra totals row in the underlying prepared file. The issue was corrected and the output retested rather than being hidden at the Tableau layer.

### 3. Scotland state and double-counting controls

An explicit Scotland reporting state was introduced in the prepared data. `All` values were removed from the relevant geography-filter design where they could overlap with the Scotland aggregate and create double-counting risk.

### 4. Stakeholder decision to consolidate KIS

Review discussions led to a clear design change: rather than maintain separate KIS Accesses and KIS Patients dashboard pages, the reporting should use one **Key Information Summary Dashboard** with a selector that switches analytical perspective.

This became the `KIS View` parameter used in the final workbook.

### 5. Combined R workflow finalised

The original R preparation script was created within the team by a colleague and had already been used to supply the separate dashboard views. When the sources needed to be combined, I became directly involved in finalising that existing workflow.

My contribution included:

- understanding the shared reporting grain;
- checking join-key fields and data types;
- replacing a one-direction join approach with a full join so source-only records were retained;
- adding/strengthening duplicate-key checks;
- adding/strengthening measure-total reconciliation;
- investigating row-count changes and lookup behaviour;
- rerunning and comparing outputs until the combined source reconciled.

This was not a rewrite from scratch. It demonstrates the ability to read, debug and complete an existing analytical pipeline safely.

## Combined-source QA

The first validated combined output contained **95,714 rows**:

| QA category | Rows |
| --- | ---: |
| Matched rows | 88,784 |
| Patient-only rows | 6,278 |
| Access-only rows | 652 |
| **Total** | **95,714** |

The source-only groups confirmed why a full join was necessary: a left join could silently discard valid records depending on join direction.

Further QA identified a duplicate geography lookup state for one practice. The issue propagated across monthly rows and the Scotland copy, inflating the combined file by **70 rows**.

After correction, the final output contained:

| QA category | Rows |
| --- | ---: |
| Matched rows | 88,714 |
| Patient-only rows | 6,278 |
| Access-only rows | 652 |
| **Total** | **95,644** |

The corrected file therefore removed the 70 duplicate rows while preserving the patient-only and access-only groups and produced **zero duplicate combined join keys**.

The specific local practice identity is intentionally omitted from the public portfolio because it is not needed to demonstrate the QA method.

## Measure reconciliation

Structural join checks were followed by numerical checks. Core patient and access measures were summed again after the full join and compared with their totals in the original prepared sources.

Conceptually:

```text
original source total
        ↓
combined-source total
        ↓
investigate if not equivalent
```

This prevents a structurally valid-looking file from passing QA when rows or measures have been duplicated or lost.

## Cross-check against established Tableau views

After the combined source was corrected, equivalent selections were checked against the earlier KIS Accesses and KIS Patients dashboards.

Small changes associated with removal of duplicated lookup records were expected and investigated. Unexplained changes were not treated as acceptable simply because the combined file refreshed successfully.

## Final Tableau validation

The final dashboard checks include:

- `KIS View` switches between the Accesses and Patients analytical states;
- `KIS Access Measure` switches the Access trend across NHS24, OOH, Portal, SAS and Other;
- the selected Access trend agrees with the corresponding monthly table values;
- the `Month` helper produces chronological monthly ordering;
- Active KIS Patients and Total KIS Patients use the same reporting context;
- Financial Year, Health Board, HSCP, Cluster and Practice filters behave consistently;
- relevant-value filtering does not expose unrelated lower-level selections;
- Home, Go To, Help and Information components work as part of the delivered dashboard;
- current Scotland-level screenshots reflect the corrected combined source.

The team has confirmed that the current workbook is connected to the **latest corrected KIS file with the expected figures**, closing the earlier source-version concern.

## Stakeholder-led iteration

Retained development notes show discussion around:

- consistent dropdown/filter terminology;
- NHS Health Board naming;
- Cluster/practice lookup quality;
- combining Accesses and Patients;
- questions about accessor/location-code information;
- whether more granular new-KIS measures could be supported by the available source;
- dashboard usage/analytics questions;
- chart/table layout and presentation.

Not every idea became delivered functionality. The portfolio distinguishes **implemented changes** from exploratory questions so it does not claim capabilities that the available data did not support.

## Implemented refinements evidenced

The retained evidence supports the following completed changes:

- Accesses and Patients consolidated into one parameter-driven dashboard;
- Financial Year and Practice terminology standardised;
- KIS capitalisation corrected;
- NHS Health Board labels standardised;
- explicit Scotland reporting state introduced;
- overlapping `All` states removed where they created double-counting risk;
- Cluster and Practice filters configured to show relevant values;
- chart/table/legend presentation refined;
- source totals-row issue corrected;
- full-join combined source introduced;
- duplicate lookup inflation found and removed;
- duplicate-key and source-total QA added around the combined output.

## Governance validation

The public case study does not publish:

- local practice-level analytical results;
- record-level source information;
- the operational R script;
- internal paths, credentials or infrastructure details;
- Tableau workbook/extract files.

Public analytical screenshots are restricted to **Scotland-level aggregate states**. Technical configuration screenshots are included only where they demonstrate implementation without disclosing local analytical results.

## What this history demonstrates

The KIS development path shows a realistic BI lifecycle:

```text
separate reports
    ↓
standardise presentation and filters
    ↓
trace reporting anomalies back to source data
    ↓
respond to stakeholder request to consolidate
    ↓
work with existing R rather than start over
    ↓
reason about join grain and source-only records
    ↓
find and remove duplicate lookup inflation
    ↓
add defensive QA
    ↓
reconcile to known-good views
    ↓
release one simpler Tableau experience
```

That combination of reporting design, code-reading, data investigation and QA is the central technical story of the KIS case study.
