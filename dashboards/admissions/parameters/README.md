# Admissions Dashboard — Parameters

The Admissions Dashboard uses two Tableau parameters to control the main analytical experience. Together they allow one workbook view to support multiple time periods and measures without duplicating dashboard pages.

## Time Window

The **Time Window** parameter allows the user to switch the pre-death analytical period between:

- 7 Days
- 14 Days
- 3 Months
- 6 Months
- 12 Months

The selected value is consumed by reusable calculated fields for:

- admissions;
- patients;
- bed days;
- deaths.

Those selected measures then feed the derived calculations used elsewhere in the workbook.

The 7-day option was added later in development following stakeholder review, demonstrating why a parameter-driven architecture was useful: the additional period could be incorporated into the existing calculation pattern instead of requiring a new dashboard.

[View Time Window parameter screenshot](01-time-window.png)

## Trend Selector

The **Trend Selector** changes the primary analytical trend between:

- Admissions Per Death
- Average Length of Stay

This control separates the question being asked from the dashboard layout. The same filter context, time window, summary table and supporting interface can be retained while the user switches the principal trend measure.

[View Trend Selector parameter screenshot](02-trend-selector.png)

## Combined behaviour

```text
Time Window
    ↓
Selected period-specific activity measures
    ↓
Derived calculations
    ↓
Trend Selector
    ↓
Admissions per Death OR Average Length of Stay
```

This parameter pattern is central to the dashboard's reusable design and is documented further in [Calculated Fields](../calculated-fields/README.md).
