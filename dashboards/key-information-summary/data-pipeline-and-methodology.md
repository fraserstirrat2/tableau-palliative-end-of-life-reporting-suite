# Key Information Summary — Data Pipeline and Methodology

This page will document the analytical path from the governed source data to the Tableau-ready output used by the **Key Information Summary** dashboard.

## Ownership boundary

Separate clearly:

- upstream/team-owned data preparation or production logic;
- any R/SQL/data-preparation work personally contributed;
- the Tableau reporting layer personally developed or maintained.

Do not infer ownership from the presence of a script or dataset.

## Pipeline to document

```text
Source data / team analytical process
        ↓
Prepared reporting output
        ↓
Validation / reconciliation
        ↓
Tableau data source
        ↓
KIS dashboard
```

## Evidence to capture

- source/output type and reporting grain;
- reporting years and geography coverage;
- key measures and definitions;
- joins/transformations relevant to interpretation;
- refresh/update process at a safe high level;
- caveats and data-quality considerations;
- what is calculated upstream versus in Tableau.

## Public portfolio rule

Explain methodology at a level that demonstrates analytical understanding without publishing restricted data, internal code, credentials, paths or infrastructure details.