# Checkbox

## Overview

**Checkbox** is a single toggleable control that lets a user mark an option as checked or unchecked. It pairs a visual tick box with an optional text label and supports the same semantic colour themes and visual variants as other input components.

---

## Properties

| **Property** | **Type** | **Default** | **Description** |
| --- | --- | --- | --- |
| **Label** (`inputLabel`) | Text | *(unset)* | Text displayed alongside the checkbox. |
| **Is the checkbox checked?** (`checked`) | Boolean | *(unset)* | The initial checked state. Bind to a page variable or data value to control it programmatically. |
| **Label Location** (`labelLocation`) | Enum | `right` | Where the label appears relative to the box. |
| **Label Size** (`labelSize`) | Enum | `fit` | Width of the label. |
| **Checkbox Size** (`size`) | Enum | `md` | Controls the dimensions of the tick box. |
| **Theme** (`checkboxTheme`) | Enum | `neutral` | Semantic colour applied to the checked state. |
| **Style** (`variant`) | Enum | `solid` | Visual treatment of the tick box. |

---

### Label Location Options

| **Value** | **Layout** |
| --- | --- |
| `top` | Label above the tick box |
| `left` | Label to the left of the tick box |
| `right` | Label to the right of the tick box *(default)* |

---

### Size Options

The tick box dimensions are calculated from the theme's text and spacing scales:

| **Value** | **Approximate size** |
| --- | --- |
| `sm` | `text.xs` + 2× `spacing.xxxs` |
| `md` | `text.sm` + 2× `spacing.xxs` |
| `lg` | `text.md` + 2× `spacing.xs` |

---

### Theme Options

`primary` · `secondary` · `neutral` · `alert` · `error` · `success`

Applies to the checked state colour — the box fill, border, or tick colour depending on the variant.

---

### Variant Options

| **Value** | **Unchecked appearance** | **Checked appearance** |
| --- | --- | --- |
| `solid` | Light tinted background | Deep filled background with white tick *(default)* |
| `subtle` | Light tinted background | Light tinted background, darker tick |
| `outline` | Transparent with coloured border | Transparent with coloured border, dark tick |
| `ghost` | Transparent, no border | Transparent, dark tick visible |

---

## Variables

| **Variable** | **Type** | **Exposed** | **Description** |
| --- | --- | --- | --- |
| `isChecked` | Boolean | ✅ Yes | Current checked state. Initialised from the `checked` prop. Read from outside via `components.checkboxId.vars.isChecked`. |

---

## Events

| **Event** | **Fires when…** | **Payload** |
| --- | --- | --- |
| `committedChange` | User checks or unchecks the box | `value`, `componentId`, `componentName`, `timestamp` |
| `click` | User clicks the checkbox area | — |
| `doubleClick` | User double-clicks | — |
| `mouseEnter` | Pointer enters | — |
| `mouseLeave` | Pointer leaves | — |

> ***Use `committedChange` in workflows** to respond to the user toggling the checkbox. Read the resulting state from `components.checkboxId.vars.isChecked` rather than from the event payload, as `isChecked` always reflects the current truth.*
> 

---

## Style Properties

| **Property** | **Default** |
| --- | --- |
| `background` | `transparent` |
| `width` | `auto` |
| `minWidth` | `auto` |
| `maxWidth` | `auto` |
| `rowGap` | `0px` |
| `columnGap` | Scales with `size` and `labelLocation` |

---

## Key Points

- **The visible tick box is not a native `<input type="checkbox">`** — the actual `<input>` is hidden and the styled box is rendered separately. This allows full visual customisation while retaining the underlying boolean state.
- **`isChecked` is the source of truth.** Always read the current state from `components.checkboxId.vars.isChecked`, not from the `checked` prop (which only sets the initial value).
- **Do not create a page variable to mirror `isChecked`.** Read it directly from the component variable. Only create a page variable if you need to store the value after a form submission.

##