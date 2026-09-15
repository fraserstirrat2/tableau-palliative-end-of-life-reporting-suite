# Service Utilisation — Data Pipeline and Methodology

This page will document the analytical path from the governed source data to the Tableau-ready Service Utilisation output.

## Ownership boundary

Separate upstream/team-owned processing from any R/SQL/data-preparation work personally contributed and from the Tableau reporting layer.

## Pipeline to document

```text
Source data / team analytical process
        ↓
Prepared service-utilisation output
        ↓
Validation / reconciliation
        ↓
Tableau data source
        ↓
Service Utilisation dashboard
```

## Evidence to capture

- source/output type and grain;
- reporting years/geographies;
- service-use measures and definitions;
- relevant transformation/aggregation logic;
- refresh/update process at a safe high level;
- data-quality caveats;
- upstream versus Tableau calculations.

Do not publish restricted source data, internal code, credentials or operational paths.