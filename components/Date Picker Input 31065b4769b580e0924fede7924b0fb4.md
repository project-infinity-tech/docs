# Date Picker Input

## Overview

A date selector that opens a calendar dropdown. Displays the selected date as a formatted string on a trigger button.

### Properties

| **Property** | **Default** | **Description** |
| --- | --- | --- |
| `inputLabel` | *(unset)* | Field label |
| `placeholder` | `"Pick a date"` | Shown when no date is selected |
| `dateFormat` | `medium` | How the selected date is displayed on the trigger button |
| `size` | `md` | Size of the trigger button |
| `labelLocation` | `top` | Label placement |
| `labelSize` | `fit` | Label width |

### Date Format Options

| **Value** | **Example output** |
| --- | --- |
| `short` | `25/12/2025` |
| `medium` | `25 Dec 2025` |
| `long` | `25 December 2025` |
| `full` | `25 December 2025` |
| `iso` | `2025-12-25` |
| `relative` | `Today` / `Tomorrow` / `Yesterday` / `In 3 days` / `2 days ago` / falls back to `medium` |

### Variables

| **Variable** | **Type** | **Exposed** | **Description** |
| --- | --- | --- | --- |
| `selectedDate` | Datetime | ✅ | The selected date as a Temporal datetime value. Access fields: `.day`, `.month`, `.year`. |

Read the selected date: `components.datepickerId.vars.selectedDate`

For database storage, use the `.year`, `.month`, and `.day` fields to construct a date string, or pass the value directly to a SQL query with a `::date` cast.

### Events

| **Event** | **Fires when…** |
| --- | --- |
| `dateChange` | The user selects a date from the calendar |