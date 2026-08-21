# Selected Activity Measures

This group contains the four reusable Tableau calculations controlled by the **Time Window** parameter:

- Selected Admissions
- Selected Beddays
- Selected Deaths
- Selected Patients

## How the pattern works

The upstream analytical dataset contains separate fields for each reporting window. Rather than placing those fields directly onto separate dashboards, Tableau uses the Time Window parameter to return the matching measure dynamically.

For example, **Selected Admissions** maps:

```text
7 Days   → 7-day admission field
14 Days  → 14-day admission field
3 Months → 3-month admission field
6 Months → 6-month admission field
12 Months → 12-month admission field
```

The same pattern is repeated for deaths, patients and bed days.

This is the main bridge between the upstream analytical structure and the interactive Tableau layer: the data can retain period-specific measures while the user experiences one consistent reporting interface.

## Why this matters

This design supports:

- one dashboard instead of five near-duplicate period-specific dashboards;
- reusable derived measures such as Admissions per Death;
- consistent behaviour in the trend chart and summary table;
- easier extension when a new analytical period is added.

The later addition of the **7-day** period is a useful example. Once the upstream measure existed, it could be incorporated into the existing Time Window pattern rather than requiring a separate dashboard architecture.

## Evidence

- [Selected Admissions](01-selected-admissions.png)
- [Selected Beddays](02-selected-beddays.png)
- [Selected Deaths](03-selected-deaths.png)
- [Selected Patients](04-selected-patients.png)
