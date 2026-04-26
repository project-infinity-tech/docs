# Chip Group

## Overview

**Chip Group** renders a set of chips from an array of options, with built-in single or multi-select behaviour. It is the standard way to build filter bars, tag selectors, and segmented choice controls without wiring up individual chips manually.

---

## Properties

| **Property** | **Type** | **Default** | **Description** |
| --- | --- | --- | --- |
| **Option Items** (`optionItems`) | Array of objects | *(unset)* | The chips to display. Each item defines a `label`, a `value`, and optional `leadingIcon` and `trailingIcon`. |
| **Label** (`inputLabel`) | Text | `"Label:"` | Optional label displayed above or beside the group. |
| **Label Location** (`labelLocation`) | Enum | `top` | Whether the label appears above (`top`) or to the left (`left`) of the chips. |
| **Label Size** (`labelSize`) | Enum | `full` | Width of the label when positioned to the left. |
| **Chip Size** (`chipSize`) | Enum | `md` | Size of every chip in the group. |
| **Theme** (`chipGroupTheme`) | Enum | `primary` | Colour theme applied to all chips. |
| **Selectable Chips?** (`selectable`) | Boolean | `false` | When on, chips can be selected. Clicking emits `committedChange` instead of `click`. |
| **Allow Multiple Selection** (`allowMultiple`) | Boolean | `false` | When on, multiple chips can be selected simultaneously. When off, selecting one deselects all others. |
| **Show Icons?** (`showIcons`) | Boolean | *(unset)* | Whether to render leading icons from `optionItems`. |

---

### Option Items Structure

Each object in `optionItems` supports:

| **Field** | **Type** | **Required** | **Description** |
| --- | --- | --- | --- |
| `label` | Text | ✅ | Display text of the chip |
| `value` | Text | ✅ | Unique identifier, returned on selection |
| `leadingIcon` | Icon name | Optional | Icon before the label |
| `trailingIcon` | Icon name | Optional | Icon after the label |

---

## Variables

| **Variable** | **Type** | **Exposed** | **Description** |
| --- | --- | --- | --- |
| `selectedItemValue` | Text | ✅ Yes | The `value` of the currently selected chip (single-select mode). |
| `selectedItemValues` | Text array | ✅ Yes | Array of `value` strings for all selected chips (multi-select mode). |

Read these from expressions or workflows:

- Single select: `components.groupId.vars.selectedItemValue`
- Multi select: `components.groupId.vars.selectedItemValues`

---

## Events

| **Event** | **Fires when…** | **Payload** |
| --- | --- | --- |
| `committedChange` | A chip is selected or deselected (when `selectable` is on) | `newValue`, `oldValue`, `componentId`, `componentName`, `timestamp` |
| `click` | Group area is clicked (when `selectable` is off) | — |
| `doubleClick` | Group area is double-clicked | — |
| `mouseEnter` | Pointer enters the group | — |
| `mouseLeave` | Pointer leaves the group | — |
| `contextMenu` | Group is right-clicked | — |

---

## Key Points

- **Single vs multi-select is controlled by `allowMultiple`.** In single-select mode, `selectedItemValue` holds the active value. In multi-select mode, `selectedItemValues` holds an array of all active values.
- **`selectable` must be on for selection to work.** If `selectable` is off, chips render as display-only labels and emit `click` rather than `committedChange`.
- **The group uses a Repeater internally.** Individual chips inside the group are not addressable by ID — read selections through the group's exposed variables.
- **Chips wrap automatically.** The inner container uses `flexWrap: wrap`, so a large set of chips flows naturally across multiple lines.