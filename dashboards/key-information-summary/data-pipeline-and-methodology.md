# Key Information Summary — Data Pipeline and Methodology

This page documents the analytical path that supports the **Key Information Summary (KIS)** Tableau dashboard while keeping the operational data, code and internal environment private.

The main technical challenge was not to recreate KIS measures in Tableau. It was to bring two related monthly reporting sources — **KIS Accesses** and **KIS Patients** — into a reliable combined reporting dataset without losing source-only records or inflating measures through duplicate joins.

## Ownership boundary

The original KIS R preparation script was created within the team by a colleague. I initially used that shared script to create the source outputs used by the separate Accesses and Patients dashboards.

When the reporting moved to a **combined KIS dashboard**, my contribution expanded into the analytical preparation itself. I did not rewrite the pipeline from scratch; I worked with the existing R code and data to:

- understand the source structure and join grain;
- adapt/finalise the logic required for a combined output;
- investigate duplicate and lookup behaviour;
- strengthen pre-join and post-join QA;
- validate that patient-only and access-only records were retained;
- reconcile the corrected combined source back to the previously validated dashboards.

This distinction is deliberate. The public case study demonstrates the ability to **read, debug and complete an existing analytical workflow** without presenting shared team code as solely my own work.

## Source structure

At a safe portfolio level, the pipeline starts with two families of monthly aggregate extracts:

```text
KIS Access activity extracts
KIS Patient Count extracts
```

The evidence reviewed for this case study covers financial years:

- 2021/22
- 2022/23
- 2023/24
- 2024/25

Each monthly source is assigned a consistent reporting month and financial year before the files are brought together into longer analytical tables.

Historical source files did not always use perfectly consistent field names. The R preparation therefore standardises schema differences before rows are combined. This is an important maintainability step because later Tableau logic expects one stable field structure even when source-export naming changes over time.

## Main Access measures

The Accesses source provides monthly activity including:

- KIS Accesses
- NHS24 Accesses
- OOH Accesses
- Portal Accesses
- SAS Accesses
- Other Accesses
- Monthly Difference / change context

The Accesses Tableau trend does not recreate these measures. It uses the prepared source measures and a Tableau parameter to select which access channel is displayed.

## Main Patient measures

The Patients source provides monthly measures including:

- Total KIS Patients
- Active KIS Patients
- Monthly Difference

Some additional fields present in the underlying source exports are not required by the final reporting layer and are excluded from the prepared Tableau source.

## Geography and practice enrichment

Both source families are enriched against a GP/practice lookup using the organisation/practice code as the shared identifier.

At a high level this adds the geography/practice structure needed by Tableau:

```text
Organisation / Practice
        ↓
Postcode
        ↓
HSCP
        ↓
Cluster
        ↓
Health Board
```

Health Board names are standardised so the reporting uses consistent `NHS ...` labels. Missing lookup values are handled explicitly rather than allowed to disappear silently during later joins.

The pipeline also creates an explicit **Scotland reporting state** so national reporting can be selected consistently in Tableau.

## Why `All` states were removed from key filters

Earlier KIS outputs contained `All`-type records alongside explicit Scotland/geography records. During development this was identified as a potential double-counting risk when the reporting logic also created Scotland aggregate states.

The final approach uses the explicit Scotland/geography records and does not rely on `All` values in the user-facing Health Board / HSCP filter design.

## The combined-source problem

The final dashboard needed one source that supported both KIS Accesses and KIS Patients.

A simple left join was not sufficient because it would preserve every row from whichever dataset was placed on the left while potentially dropping valid rows that existed only in the other source.

The required relationship was therefore:

```text
records present in both sources
+ patient-only records
+ access-only records
```

The final combination uses a **full join** at the shared reporting grain.

## Shared join grain

The combined workflow uses a shared set of reporting dimensions equivalent to:

- Organisation / Practice Code
- Organisation / Practice Name
- Health Board
- Financial Year
- Time Period
- Postcode
- HSCP
- Cluster

Before joining, the relevant key fields are normalised to compatible data types. This prevents valid records failing to match simply because one source represents an identifier as numeric while another represents it as character text.

## Duplicate-key protection

A full join is only safe if the intended key is unique at the expected reporting grain. Otherwise a many-to-many join can multiply rows and inflate measures.

The finalised workflow therefore checks both sources for duplicated joining keys **before** the combined file is produced. If duplicated keys are present, the issue must be resolved rather than allowed to flow into Tableau.

This became important during QA because the GP/practice lookup contained a duplicated geography mapping for one practice. The duplicate was repeated across monthly records and then again through the Scotland aggregation step, inflating the first combined output.

### Before correction

The first validated combined output contained:

- **95,714 rows**
- **88,784 matched rows**
- **6,278 patient-only rows**
- **652 access-only rows**

### After correction

After the duplicate geography lookup state was removed and the pipeline rerun, the final output contained:

- **95,644 rows**
- **88,714 matched rows**
- **6,278 patient-only rows**
- **652 access-only rows**
- **zero duplicate combined join keys**

The **70-row reduction** was therefore explainable rather than an unexplained shift in reporting totals.

## Why patient-only and access-only records matter

The QA split is useful because it proves that the two KIS sources are related but not perfectly one-to-one at every reporting key.

```text
Matched              88,714
Patient-only           6,278
Access-only              652
```

A left join would have risked discarding one of those valid source-only groups depending on join direction. The full join retains them explicitly.

## Measure-total reconciliation

The combined workflow does not treat successful row joining as sufficient QA. After the full join, key measures from each original source are summed again in the combined output and compared with the original totals.

Patient-side checks include the core patient totals and monthly-difference measure. Access-side checks include the main access channels, total KIS access activity and monthly-difference context.

Conceptually:

```text
source total
    ↓ compare
combined-source total
    ↓
pass only when equivalent
```

This protects the Tableau layer from subtle data loss or duplication even when a joined file appears structurally valid.

## Separate outputs retained as QA references

The original KIS Accesses and KIS Patients dashboards became valuable regression references during the consolidation work.

After the combined source was corrected, equivalent selections in the new workbook were checked against the established separate views. Small differences associated with removing duplicate lookup records were expected and investigated; unexplained differences were not accepted as normal.

This is a useful example of using an existing production/reporting view as a **known-good comparison point** while replacing the underlying architecture.

## Final pipeline

```text
Monthly KIS Access extracts
        ↓
monthly standardisation + financial-year assembly
        ↓
GP / geography lookup enrichment
        ↓
Health Board naming + missing-value handling
        ↓
Scotland reporting state
        ↓
Accesses prepared dataset

Monthly KIS Patient Count extracts
        ↓
monthly standardisation + financial-year assembly
        ↓
GP / geography lookup enrichment
        ↓
Health Board naming + missing-value handling
        ↓
Scotland reporting state
        ↓
Patients prepared dataset

Accesses prepared dataset + Patients prepared dataset
        ↓
join-key type standardisation
        ↓
duplicate-key checks
        ↓
full join at shared reporting grain
        ↓
matched / patient-only / access-only diagnostics
        ↓
measure-total reconciliation
        ↓
combined Tableau-ready KIS source
        ↓
KIS View + Access Measure interaction layer
        ↓
final Tableau dashboard
```

## What is upstream versus Tableau logic

### Prepared upstream / R layer

- monthly source ingestion;
- schema harmonisation;
- financial-year assembly;
- GP/practice geography enrichment;
- missing-value treatment;
- Scotland reporting rows;
- combined Accesses/Patients source;
- duplicate-key QA;
- source-total reconciliation.

### Tableau layer

- Month helper used for chronological monthly display;
- KIS View switching;
- access-measure selection;
- Access trend;
- Access detail table;
- Patients trend;
- shared Financial Year / geography / Practice filters;
- Information / Help / Home / Go To interface;
- dashboard-level validation and presentation.

## Public portfolio rule

The repository does not publish the operational R script, the source extracts, the GP/practice lookup, local-level outputs, internal paths or credentials.

The methodology is documented at a level that demonstrates:

- understanding of existing R code;
- data-grain and join reasoning;
- data-quality investigation;
- defensive QA design;
- traceability from prepared source to Tableau;

without exposing governed organisational artefacts.
