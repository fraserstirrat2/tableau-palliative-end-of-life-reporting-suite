# Key Information Summary — Calculated Fields

The supplied KIS evidence contains five relevant Tableau calculated/helper fields. The calculation layer is intentionally compact: the heavier data-combination and QA logic is handled upstream, while Tableau focuses on monthly display, view switching and selected-measure interaction.

## Calculation inventory

| Field | Purpose | Main dependency | Evidence |
| --- | --- | --- | --- |
| `Month` | Converts text reporting period into a true date for chronological axes | `Time Period` | `01-Month.png` |
| `Access Monthly Difference` | Readable Access monthly-change field for reporting/table use | combined-source monthly-difference field | `02-Access-Monthly-Difference.png` |
| `KIS View Filter` | Carries the KIS View selection into worksheet filtering | `KIS View` parameter | `03-KIS-View-Filter.png` |
| `Patient Monthly Difference` | Readable Patient monthly-change field | combined-source monthly-difference field | `04-Patient-Monthly-Difference.png` |
| `Selected KIS Accesses` | Returns the selected access channel for the Access trend | `KIS Access Measure` parameter | `05-Selected-KIS-Accesses.png` |

## `Month`

**Purpose:** create a genuine Tableau date from the source `Time Period` text field.

The calculation extracts the year from the reporting-period text, maps the month abbreviation to a month number and constructs a date.

Conceptually:

```text
"April 2024"
      ↓
month = 4
reporting year = 2024
      ↓
Tableau date
      ↓
chronological monthly axis
```

This avoids alphabetical month ordering and makes the time-series worksheets behave consistently across financial years.

## `Access Monthly Difference`

**Purpose:** expose the Access-side monthly-change field under a readable Tableau name after the Accesses and Patients datasets were combined.

The combined source creates suffixed fields where the two inputs contain similarly named columns. The wrapper keeps the workbook/reporting layer understandable without requiring worksheet authors to work directly with implementation suffixes.

## `KIS View Filter`

The supplied calculation is a direct reference to the `KIS View` parameter.

```text
[KIS View]
```

It is then used on the analytical worksheets as a filter/helper so the dashboard can coordinate the Accesses and Patients states.

### Why it exists

The field separates the user-facing parameter from worksheet filter configuration. This is a common pattern in parameter-driven Tableau designs because it gives one reusable field that can be applied consistently across the relevant sheets.

## `Patient Monthly Difference`

**Purpose:** expose the Patient-side monthly-change field under a readable name in the reporting layer.

Like the Access wrapper, it protects the Tableau design from relying directly on the less-readable suffixed source-field naming created during the data combination.

The public case study documents the analytical role of the wrapper rather than relying on suffix labels as business terminology.

## `Selected KIS Accesses`

This is the key measure-selection calculation for the Access trend.

The supplied evidence shows the following logic:

```text
CASE [KIS Access Measure]
WHEN 1 THEN SUM([NHS24 Accesses])
WHEN 2 THEN SUM([OOH Accesses])
WHEN 3 THEN SUM([Portal Accesses])
WHEN 4 THEN SUM([SAS Accesses])
WHEN 5 THEN SUM([Other Accesses])
END
```

### Why it exists

Without this calculation, the workbook could require a separate trend worksheet for each access channel.

Instead:

```text
KIS Access Measure parameter
        ↓
Selected KIS Accesses
        ↓
one reusable Access trend worksheet
```

This is a simple but effective example of reducing duplicated Tableau objects through parameter-driven measure selection.

## Source fields versus Tableau calculations

The following measures are **prepared source measures**, not calculations recreated in Tableau:

- KIS Accesses
- NHS24 Accesses
- OOH Accesses
- Portal Accesses
- SAS Accesses
- Other Accesses
- Active KIS Patients
- Total KIS Patients

The Tableau calculation layer primarily controls **selection, naming and display behaviour**.

That distinction matters because the public portfolio should not suggest that core KIS measures were mathematically rederived in Tableau when they were supplied by the governed preparation workflow.

## Evidence note

The monthly-difference screenshots reflect the workbook's combined-source field structure. The public documentation intentionally focuses on the semantic Access/Patient wrapper names rather than treating `.x` / `.y` suffixes as business logic.
