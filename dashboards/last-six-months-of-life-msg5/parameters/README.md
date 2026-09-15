# MSG5 — Parameters and User Controls

This folder documents the two parameters that drive the **Last 6 Months of Life by Setting** dashboard.

## 1. Bed Days

The main user-facing display selector is the **Bed Days** parameter.

![Bed Days parameter](01-bed-days.png)

### Configuration

| Property | Value |
| --- | --- |
| Name | `Bed Days` |
| Data type | Integer |
| Allowable values | Fixed list |
| Current value in supplied evidence | Numbers |
| Value when workbook opens | Current value |

### Values

| Stored value | Display value |
| ---: | --- |
| `1` | Numbers |
| `2` | Percentages |

### Reporting role

The parameter lets the user switch the same dashboard between:

```text
Bed Days = 1 / Numbers
        ↓
absolute bed-day stacked bar + table
```

and:

```text
Bed Days = 2 / Percentages
        ↓
percentage-distribution stacked bar + table
```

A calculated field named **`BedDaysView_Filter`** returns the active parameter value and is used within the worksheet filter architecture so the appropriate worksheet pair is shown.

This is a good example of using a simple parameter to keep one reporting interface while allowing different measure formats and worksheet formatting behind it.

## 2. Council Area

The second user-facing parameter is **Council Area**.

![Council Area parameter](01-council-area.png)

### Configuration

| Property | Value |
| --- | --- |
| Name | `Council Area` |
| Data type | String |
| Allowable values | Fixed list |
| Current value in supplied evidence | Scotland |
| Value when workbook opens | Current value |

The visible list includes **Scotland** plus the available Council Area reporting geographies.

### Reporting role

The parameter allows the managed workbook to reuse the same dashboard structure for the Scotland aggregate and Council Area reporting states.

It is supported by:

- `Council Area`
- `Is Selected Council (Filter)`

These calculations compare the selected parameter value with the source geography field and include explicit handling for Scotland and the guarded `Select` state.

The public portfolio demonstrates this technical pattern but publishes **Scotland-level analytical output only**.

## Parameter-to-dashboard architecture

```text
Council Area parameter
        ↓
Council Area / Is Selected Council calculations
        ↓
selected reporting geography

Bed Days parameter
        ↓
BedDaysView_Filter
        ↓
Numbers OR Percentages worksheet pair
```

## Public evidence rule

The screenshots in this folder demonstrate configuration only. They should not be used to publish local-area analytical results. The case study remains within the agreed Scotland-level public boundary.
