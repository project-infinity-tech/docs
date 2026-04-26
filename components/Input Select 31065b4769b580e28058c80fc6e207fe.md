# Input Select

## Input Select

**Component ID:** `pla_inputselect`

A dropdown selector for choosing one item (or multiple items) from a predefined list. Renders a trigger button that opens a popover list when clicked.

### Properties

| **Property** | **Default** | **Description** |
| --- | --- | --- |
| `label` | *(unset)* | Field label |
| `placeholder` | `"Select an item"` | Shown when nothing is selected |
| `optionList` | *(unset)* | Array of options. Each item has `label` (display text), `value` (identifier), and optional `icon`. |
| `defaultValue` | *(unset)* | Pre-selected item `{index, value, label}` |
| `allowMultiple` | `false` | Allow selecting more than one item at once |
| `labelLocation` | `top` | Label placement |
| `labelSize` | `full` | Label width |
| `position` | `bottom-start` | Where the dropdown appears relative to the trigger |
| `matchTriggerWidth` | `true` | Dropdown matches the width of the trigger button |
| `autoPosition` | `false` | Automatically reposition if the dropdown would overflow the viewport |
| `offset` | `theme.spacing.xxs` | Gap between trigger and dropdown |
| `showPopoverContent` | `false` | Preview the dropdown open state in the editor |

### Option List Structure

```
[
  { "label": "Option A", "value": "a" },
  { "label": "Option B", "value": "b", "icon": "Star" }
]
```

`label` is the display text; `value` is what gets stored and returned. If `label` is omitted, `value` is displayed.

### Variables

| **Variable** | **Type** | **Exposed** | **Description** |
| --- | --- | --- | --- |
| `selectedItems` | Array of `{index, value, label}` | ✅ | All currently selected items. In single-select mode, this array always has 0 or 1 items. |
| `dropdownOpen` | Boolean | ✅ | Whether the dropdown is currently open |

Read the selected value: `components.selectId.vars.selectedItems[0]?.value`

### Events

Input Select has **no events**. React to selections by reading `vars.selectedItems` from other workflows, or use a `SetVariable` step triggered by `vars.dropdownOpen` changing to `false`.