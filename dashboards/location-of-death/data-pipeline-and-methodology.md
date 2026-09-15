# Location of Death — Data Pipeline and Methodology

This page will document the analytical path from the governed source data to the Tableau-ready Location of Death output.

## Ownership boundary

Separate upstream/team-owned preparation from any R/SQL/data-processing work personally contributed and from the Tableau reporting layer.

## Pipeline to document

```text
Source data / team analytical process
        ↓
Prepared location-of-death output
        ↓
Validation / reconciliation
        ↓
Tableau data source
        ↓
Location of Death dashboard
```

## Evidence to capture

- source/output type and grain;
- reporting years/geographies;
- location categories and measure definitions;
- relevant transformation/aggregation logic;
- refresh/update process at a safe high level;
- data-quality/reporting caveats;
- upstream versus Tableau calculations.

Do not publish restricted source data, internal operational code, credentials or paths.