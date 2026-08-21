# Trend-Selection Logic

This group contains the calculation used to connect the **Trend Selector** parameter to the measure displayed in the main analytical trend area:

- Trend Selector Filter

## Purpose

The Trend Selector allows the reporting question to change without duplicating the dashboard layout. The user can switch between:

- Admissions Per Death
- Average Length of Stay

The same Time Window, filter context, Scotland comparator and summary-table structure can therefore be retained while the main trend measure changes.

[View Trend Selector Filter evidence](01-trend-selector-filter.png)

This is part of the wider reusable architecture documented in [Calculated Fields](../README.md) and [Parameters](../../parameters/README.md).
