# Divider

## Overview

**Divider** renders a thin line used to visually separate sections of content. It can run horizontally (across the full width of its container) or vertically (the full height of its container), and its colour, thickness, and surrounding spacing are all configurable.

---

## Properties

| **Property** | **Type** | **Default** | **Description** |
| --- | --- | --- | --- |
| **Direction** (`direction`) | Enum | `horizontal` | Whether the line runs left-to-right or top-to-bottom. |
| **Divider Width** (`dividerSize`) | Text | `1px` | The thickness of the line itself. Despite the label saying "width", this controls the thin dimension of the line — its height when horizontal, its width when vertical. |
| **Colour** (`color`) | Colour | `neutral[100]` | The colour of the line. Accepts theme colour expressions or hex values. |
| **Vertical Spacing** (`dividerVerticalSpacing`) | Dimension | `theme.spacing.sm` | Padding applied above and below the divider. Controls the breathing room between the line and surrounding content. |
| **Horizontal Spacing** (`dividerHorizontalSpacing`) | Dimension | *(unset)* | Padding applied to the left and right of the divider. Useful when you want the line to be inset from the edges of its container. |

---

### Direction Options

| **Value** | **Behaviour** |
| --- | --- |
| `horizontal` | Line spans the full width of its container. Height is determined by `dividerSize`. |
| `vertical` | Line spans the full height of its container. Width is determined by `dividerSize`. |

---

## Sizing Behaviour

The outer wrapper automatically sizes itself to match the chosen direction:

- **Horizontal:** wrapper is `width: 100%`, height is `auto`
- **Vertical:** wrapper is `height: 100%`, width is `fit-content`

This means a horizontal Divider will naturally stretch to fill whatever column it sits in, and a vertical Divider will stretch to match the height of its siblings in a row.

---

## Events

| **Event** | **Fires when…** |
| --- | --- |
| `click` | User clicks the divider |
| `doubleClick` | User double-clicks the divider |
| `mouseEnter` | Pointer enters the divider area |
| `mouseLeave` | Pointer leaves the divider area |

---

## Key Points

- **The line is a `<hr>` element** with `border: none`, rendered purely via background colour and dimensions. It has slightly rounded ends (`border-radius: 99rem`).
- **`dividerSize` is the thickness**, not the length. The length is always determined by the container (`100%` in the relevant axis).
- **Vertical spacing controls the gap** between the divider and the content above and below it. Increase `dividerVerticalSpacing` to give sections more room to breathe; reduce it for tighter layouts.
- **For vertical use**, the Divider must be placed inside a `row`direction Container alongside the elements it separates, and that container should have a defined height for the `height: 100%` to take effect.
- **The default colour (`neutral[100]`)** is very light and subtle. For more visible separators, use `neutral[200]` or `neutral[300]`.