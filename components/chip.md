# Chip

## Overview

**Chip** is a compact, pill-shaped label used to display status badges, category tags, metadata, and filterable selections. It supports the same semantic colour themes and visual variants as buttons, optional leading and trailing icons, and a selectable mode that turns it into a toggleable control.

---

## Properties

| **Property** | **Type** | **Default** | **Description** |
| --- | --- | --- | --- |
| **Content** (`content`) | Text | *(unset)* | The label text displayed inside the chip. |
| **Size** (`size`) | Enum | `md` | Controls the overall height and text size. |
| **Theme** (`chipTheme`) | Enum | `neutral` | Semantic colour applied to the chip. |
| **Variant** (`variant`) | Enum | `subtle` | Visual weight — how prominently the colour is applied. |
| **Leading Icon** (`leadingIcon`) | Icon name | *(unset)* | Optional icon displayed before the label text. |
| **Trailing Icon** (`trailingIcon`) | Icon name | *(unset)* | Optional icon displayed after the label text. |
| **Selectable** (`selectable`) | Boolean | `false` | When on, clicking the chip toggles its `active` state and emits a `select` event instead of a `click` event. |
| **Value** (`value`) | Text | *(unset)* | An identifier for this chip, used when reading which chip was selected from a workflow. |

---

### Size Options

| **Value** | **Height** | **Font size** |
| --- | --- | --- |
| `sm` | `text.xs` + 2× `spacing.xxxs` | `text.sm` |
| `md` | `text.sm` + 2× `spacing.xxs` | `text.md` |
| `lg` | `text.md` + 2× `spacing.xs` | `text.lg` |

---

### Theme Options

`primary` · `secondary` · `neutral` · `alert` · `error` · `success`

These follow the same semantic colour system as buttons and alerts — use `success` for positive states, `error` for destructive or failed states, `alert` for warnings, and `neutral` for generic tags.

---

### Variant Options

| **Value** | **Appearance** |
| --- | --- |
| `solid` | Fully filled background. Light text on a deep colour. Highest visual weight. |
| `outline` | Transparent background with a coloured border and dark text. |
| `subtle` | Lightly tinted background with a faint border and dark text. *(default)* |
| `ghost` | No background or border until hovered. Text only. Lowest visual weight. |

---

## Variables

| **Variable** | **Type** | **Exposed** | **Description** |
| --- | --- | --- | --- |
| `active` | Boolean | ✅ Yes | Whether the chip is currently selected. Read from outside the chip via `components.chipId.vars.active`. Toggled automatically when `selectable` is on and the chip is clicked. |

---

## Events

| **Event** | **Fires when…** |
| --- | --- |
| `click` | Chip is clicked (when `selectable` is **off**) |
| `doubleClick` | Chip is double-clicked |
| `mouseEnter` | Pointer enters the chip |
| `mouseLeave` | Pointer leaves the chip |
| `select` | Chip is clicked (when `selectable` is **on**). Payload contains selection data. |
| `leadingIconClick` | The leading icon is clicked |
| `trailingIconClick` | The trailing icon is clicked |

> **`*click` vs `select`:** When `selectable` is on, clicking emits `select` and toggles `vars.active`. When `selectable` is off, clicking emits `click` and `active` stays unchanged. Never wire both — only one fires depending on the mode.*
> 

---

## Selectable Mode

When `selectable` is `true`, the chip behaves as a toggle:

1. The user clicks the chip.
2. `vars.active` flips between `true` and `false`.
3. The chip's visual style updates — active chips use a deeper shade of the chosen theme colour.
4. A `select` event fires for your workflow to respond to.

Read the current state from a workflow or expression using `components.chipId.vars.active`.

---

## Key Points

- **Chips are `inline-flex`** — they size to their content and sit inline with surrounding elements. Wrap them in a flex container with `flexWrap: wrap` to create a wrapping tag cloud.
- **Leading and trailing icons are rendered as Icon Buttons** internally. This means they can receive their own `leadingIconClick` / `trailingIconClick` events independently of the chip body — useful for a "remove tag" ✕ trailing icon that doesn't also trigger a select.
- **Active state colours are baked in.** When `active` is `true`, the background shifts to a deeper shade of the theme colour automatically — you don't need to write conditional style expressions.

## --

#