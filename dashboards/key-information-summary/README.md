# Key Information Summary — Technical Case Study

This case study documents the **Key Information Summary (KIS)** dashboard within the wider palliative and end-of-life care Tableau reporting suite.

The KIS work is particularly useful as a BI case study because the final dashboard is not simply a visual redesign. It developed from **two separate reporting products — KIS Accesses and KIS Patients — into one combined Tableau experience**, supported by a shared analytical dataset, parameter-driven view switching, stronger join/duplicate QA and repeated reconciliation back to the original reporting views.

> **Portfolio status:** written technical case study complete. The current Tableau evidence has been reviewed and the documentation below reflects the final implementation and retained development history. The detailed PNG evidence is being added manually to the repository; until that upload is complete, some image links in the evidence folders may not yet resolve.

**Latest reporting year shown in the supplied Tableau evidence:** 2024/25.

## Case study at a glance

| Employer question | Evidence from this dashboard |
| --- | --- |
| **What problem was being solved?** | KIS activity was originally presented through separate Accesses and Patients dashboards. The final solution brings both into one controlled reporting interface so users can switch analytical perspective without moving between separate dashboard pages. |
| **What was my role?** | I developed and refined the Tableau reporting layer and, when the two KIS sources were combined, I also worked directly with the existing R preparation script: reading and adapting the shared code, investigating join/lookup issues, strengthening QA checks, removing duplicate inflation and validating the final combined output. |
| **What technical capability does it show?** | Parameter-driven worksheet switching, selectable access measures, multi-level filtering, dual-measure patient trends, Measure Names / Measure Values tables, date helper logic, R/data-pipeline debugging, join-grain reasoning and numerical reconciliation. |
| **How were the numbers trusted?** | The combined output was checked against the separately validated Accesses and Patients views, duplicate join keys were tested before combination, patient-only/access-only records were retained, and measure totals were reconciled after the join. |
| **How did stakeholders influence the product?** | Regular review discussions drove terminology, filter behaviour, layout and the eventual decision to combine Accesses and Patients into one KIS dashboard rather than maintain two separate reporting pages. |
| **Why does the solution matter?** | It reduces duplication, keeps related KIS measures in one reusable interface and demonstrates how reporting usability and data-pipeline reliability can be improved together rather than treated as separate problems. |

## Reporting purpose

The dashboard presents **Key Information Summary activity over time** through two user-selectable analytical states:

### KIS Accesses

The Accesses state reports monthly activity for:

- **NHS24 accesses**
- **Out of Hours (OOH) accesses**
- **Portal accesses**
- **Scottish Ambulance Service (SAS) accesses**
- **Other accesses**
- **Total KIS accesses**

A user-facing **KIS Access Measure** control determines which access type is shown in the main line trend, while the monthly table retains the wider access breakdown for context.

### KIS Patients

The Patients state presents:

- **Total KIS Patients**
- **Active KIS Patients**
- **monthly change / difference in patient numbers** as part of the supporting reporting logic

The main Patients worksheet uses the same monthly time structure and shared reporting filters as the Accesses state.

## Reporting scope and filters

The supplied evidence covers financial years from **2021/22 through 2024/25**. The final dashboard provides a common filter framework for:

- Financial Year
- Health Board
- HSCP
- Cluster
- Practice

The public portfolio uses **Scotland-level analytical states only**. The production workbook supports more detailed reporting levels, but those granular values are not published here.

## My contribution and ownership boundary

The KIS R preparation work began as **team/shared analytical code authored initially by a colleague**. I first used that existing script to produce the source outputs required for the separate KIS Accesses and KIS Patients dashboards.

My role expanded materially when the reporting was redesigned as a single combined KIS dashboard. I did **not rewrite the R pipeline from scratch**. Instead, I:

- read and understood the existing script and source structure;
- worked through how the Accesses and Patients datasets should be combined at the correct reporting grain;
- helped finalise the combined-data logic so patient-only and access-only records were not lost;
- investigated duplicate-key and lookup behaviour that was inflating the combined output;
- strengthened QA checks around join keys and retained measure totals;
- reran and inspected outputs during debugging;
- cross-checked the corrected combined dataset against the already validated separate Tableau views;
- used the final corrected source to complete the unified Tableau dashboard.

This is an important ownership distinction. The portfolio does not claim that I authored the original production R code; it demonstrates my ability to **read existing analytical code, understand data grain, diagnose join and lookup problems, add validation and finish a shared analytical workflow safely**.

The operational script itself is not published because it contains organisational implementation detail and sits within a governed team workflow.

## How the dashboard evolved

The final product is the result of several development stages rather than a one-off build.

### 1. Separate KIS Accesses and KIS Patients views

The work began with separate Tableau reporting views. Both used a common set of geography/practice dimensions and monthly financial-year reporting, but each had its own measures and presentation.

Early development focused on making those views usable and consistent, including:

- standardising Health Board naming;
- aligning filter terminology;
- changing the user-facing organisation label to **Practice**;
- standardising **Financial Year** wording;
- correcting **KIS** capitalisation;
- improving legend, chart-border and table presentation;
- configuring Cluster and Practice controls to show relevant values;
- introducing Scotland-level reporting states without relying on an `All` category that could lead to double counting.

### 2. Data-quality issues identified in the separate views

During the Patients development, an unexpected `NA` pattern was traced to a totals row in the underlying base file being treated as a normal record. The issue was corrected and the output retested.

This stage reinforced an important principle that carried into the combined solution: **reporting-layer anomalies were investigated back through the prepared data rather than being hidden with Tableau formatting**.

### 3. Stakeholder decision to combine the two KIS products

Review discussions then moved from improving two separate dashboards to asking whether KIS Accesses and KIS Patients could be presented as one product. The agreed direction was a single **Key Information Summary Dashboard** with a parameter allowing users to switch between the two analytical perspectives.

That change reduced duplicate navigation and gave the dashboard one shared filter framework, information panel and interface structure.

### 4. Combined source and QA hardening

The combined dataset required more than simply placing the two files beside one another. The final workflow had to preserve:

- records present in both sources;
- patient-only records;
- access-only records;
- the complete totals from each original dataset.

The combined logic therefore moved to a **full-join approach** at the shared reporting grain, with explicit duplicate-key checks before the join and measure-total reconciliation afterwards.

A further QA investigation identified a duplicated GP-practice geography lookup state that was inflating rows in the combined file. The first validated combined version contained **95,714 rows**. After the lookup issue was corrected, the final output contained **95,644 rows**, removing **70 duplicate rows** and leaving **zero duplicate combined join keys**.

The final diagnostic split was:

- **88,714 matched rows**
- **6,278 patient-only rows**
- **652 access-only rows**

The patient-only and access-only records are significant: retaining them is why a full join was required rather than a left join that could silently discard valid reporting activity.

### 5. Final Tableau consolidation

Once the combined output was validated, the final Tableau dashboard was built around:

- the **KIS View** parameter for Accesses / Patients switching;
- the **KIS Access Measure** parameter for access-channel selection;
- shared Financial Year, Health Board, HSCP, Cluster and Practice controls;
- a dedicated KIS Access Trend worksheet;
- a detailed KIS Access Table worksheet;
- a KIS Patients Trend worksheet;
- shared Home, Go To, Help and Information components.

The final corrected source has since been rechecked with the team and is the file currently used by the workbook.

## Analytical architecture

```text
Monthly KIS Access extracts      Monthly KIS Patient Count extracts
            ↓                                  ↓
      financial-year assembly + schema standardisation
            ↓                                  ↓
          shared GP / geography enrichment and cleaning
                         ↓
             Scotland reporting rows
                         ↓
         duplicate-key / join-grain validation
                         ↓
      full join of Accesses and Patients sources
                         ↓
   matched + patient-only + access-only diagnostics
                         ↓
        source-measure total reconciliation
                         ↓
             combined Tableau-ready output
                         ↓
      KIS View parameter + shared filter framework
                 ↙                       ↘
        KIS Accesses                  KIS Patients
                 \                       /
                  unified Tableau dashboard
                         ↓
           QA + stakeholder review + refinement
```

See [Data Pipeline and Methodology](data-pipeline-and-methodology.md) for the safe technical description of this process.

## Tableau interaction design

### KIS View

The main view selector is an integer parameter:

| Stored value | Display value |
| ---: | --- |
| `1` | KIS Accesses |
| `2` | KIS Patients |

The `KIS View Filter` calculated field carries the selected parameter value into the relevant worksheets, allowing one dashboard page to support the two analytical states.

### KIS Access Measure

The Accesses state contains a second integer parameter:

| Stored value | Display value |
| ---: | --- |
| `1` | NHS24 Accesses |
| `2` | OOH Accesses |
| `3` | Portal Accesses |
| `4` | SAS Accesses |
| `5` | Other Accesses |

`Selected KIS Accesses` uses this parameter to return the chosen access measure for the line trend.

A second workbook parameter named `KIS accesses` is also retained in the supplied workbook. The current analytical worksheet evidence shows the delivered trend logic using **KIS Access Measure**, so the retained string parameter is documented as legacy/supporting configuration rather than presented as a second active user interaction.

See [Parameters](parameters/README.md) and [Calculated Fields](calculated-fields/README.md).

## Dashboard composition

The supplied evidence confirms **three analytical worksheets**:

1. **KIS - Access Trend** — monthly line trend for the selected access type.
2. **KIS - Access Table** — monthly detail table covering access channels, total KIS activity and monthly-difference context.
3. **KIS Patients Trend** — monthly trend comparing Active KIS Patients and Total KIS Patients.

The dashboard also uses **four shared interface worksheets**:

- **HELP**
- **GO TO**
- **HOME**
- **INFO**

See [Worksheets](worksheets/README.md).

## Calculation architecture

Five calculation screenshots were supplied for the final KIS evidence set:

- `Month`
- `Access Monthly Difference`
- `KIS View Filter`
- `Patient Monthly Difference`
- `Selected KIS Accesses`

The calculations are deliberately lightweight. The complexity in this dashboard comes primarily from **combining two related reporting products and coordinating their state, filters and validated source data**, rather than from reproducing source calculations inside Tableau.

See [Calculated Fields](calculated-fields/README.md).

## Information design

The Information view explains:

- the difference between **KIS Accesses** and **KIS Patients**;
- what each access channel represents;
- the measures available in the Patients view;
- how Financial Year and geography/practice filters affect the result;
- how to switch between the two KIS states;
- how to change the selected Access measure;
- how to use chart/table hover detail.

Definitions shown in the workbook include NHS24, Out of Hours, Scottish Ambulance Service and Portal access activity. Embedding these explanations inside the reporting experience helps reduce ambiguity for users who are not familiar with the source terminology.

## Validation approach

The validation chain for the final product is:

```text
Separate validated KIS Accesses + KIS Patients outputs
        ↓
combined-source join and duplicate checks
        ↓
post-join measure reconciliation
        ↓
combined Tableau data source
        ↓
Accesses / Patients worksheet checks
        ↓
KIS View + Access Measure interaction checks
        ↓
Scotland-level dashboard states
```

The separate Accesses and Patients dashboards were valuable QA references during consolidation: once the combined file was corrected, equivalent selections in the new dashboard were cross-checked against those established views.

See [Validation and Development](validation-and-development.md) for the full history and QA evidence.

## Why this dashboard is useful

The strongest value of the KIS solution is the combination of **reporting simplification and data-quality improvement**.

Instead of maintaining two separate dashboard pages, the final product:

- gives users one route into KIS reporting;
- keeps Accesses and Patients within the same filter context;
- makes access-channel exploration explicit through a parameter;
- retains monthly detail alongside trend reporting;
- provides embedded definitions and navigation;
- reduces duplicated dashboard maintenance;
- relies on a combined source that has explicit checks for duplicate keys and retained totals.

From an employer perspective, the work demonstrates that BI delivery is not limited to visual design. It also requires understanding existing analytical code, data grain, joins, lookups, QA and how source changes affect the final reporting experience.

## Evidence in this case study

The KIS evidence package contains:

- **5 approved Scotland-level dashboard states**;
- **7 Tableau worksheet screenshots** — 3 analytical + 4 interface/navigation components;
- **3 parameter screenshots**, with 2 identified as core delivered controls and 1 retained/legacy configuration;
- **5 calculated-field screenshots**;
- detailed data-pipeline/methodology documentation;
- the combined-source QA and duplicate-removal history;
- stakeholder-led development history;
- governance and ownership boundaries.

Explore the evidence through:

- [Dashboard screenshots](dashboard-screenshots/README.md)
- [Worksheets](worksheets/README.md)
- [Parameters](parameters/README.md)
- [Calculated fields](calculated-fields/README.md)
- [Data pipeline and methodology](data-pipeline-and-methodology.md)
- [Tableau implementation](tableau-implementation.md)
- [Validation and development](validation-and-development.md)

## Governance and portfolio boundary

The production KIS workflow includes organisational source files, GP/practice-level geography lookups and operational R code. Those artefacts are **not published**.

The public case study therefore does not include:

- underlying KIS source extracts;
- GP/practice-level analytical data;
- the operational R script;
- internal file paths, credentials or infrastructure details;
- Tableau workbook/extract files;
- local or granular dashboard states outside the approved portfolio boundary.

The public evidence is restricted to **approved Scotland-level aggregate dashboard views plus technical configuration screenshots** that demonstrate Tableau implementation without publishing local results.

The repository should be read as evidence of **professional BI development, analytical debugging, Tableau implementation, quality assurance and stakeholder-led iteration**, not as a public release of the underlying KIS management-information system.
