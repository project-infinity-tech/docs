# Icon

## Overview

**Icon** displays a single vector symbol from Scram's icon libraries. Icons are used to reinforce meaning, indicate actions, and add visual interest to interfaces — alongside text labels, inside buttons, as status indicators, or as standalone visual cues.

> ***For a clickable icon that navigates to a page**, use **Icon Button** (`pla_iconbutton`) instead. The Icon component has no click event and is not intended as an interactive control.*
> 

---

## Properties

| **Property** | **Type** | **Default** | **Description** |
| --- | --- | --- | --- |
| **Icon** (`iconName`) | Icon name | *(unset)* | Which icon to display. Select from the icon picker in the editor, or provide an icon name as a text expression. |
| **Icon Size** (`iconSize`) | Enum | `md` | Controls the rendered dimensions of the icon. |
| **Just a decorative Icon?** (`decorative`) | Boolean | `false` | Whether the icon is purely visual with no informational meaning. See the Accessibility section below. |

---

### Size Options

| **Value** | **Dimensions** |
| --- | --- |
| `sm` | 16 × 16px |
| `md` | 24 × 24px *(default)* |
| `lg` | 32 × 32px |

Icons always maintain a `1/1` aspect ratio and are set to `flex: none` — they will never stretch or shrink within a flex layout.

---

## Style Properties

| **Property** | **Default** |
| --- | --- |
| `color` | `neutral[600]` |
| `width` / `height` | Driven by `iconSize` prop |
| `aspectRatio` | `1/1` |
| `background` | `transparent` |
| `opacity` | `1` |
| `borderRadius` | `0` |
| `padding` | `0` |
| `margin` | `auto` |
| `cursor` | `auto` |
| `pointerEvents` | `auto` |

**Colour** is the most commonly overridden property. Set it to any theme colour expression — for example `theme.colors.primary["500"]` for a branded icon, or `theme.colors.error["500"]` for a destructive warning icon. The default `neutral[600]` gives a mid-grey suitable for supporting icons in most contexts.

---

## Events

| **Event** | **Fires when…** |
| --- | --- |
| `mouseEnter` | Pointer moves over the icon |
| `mouseLeave` | Pointer moves away from the icon |

Icons do not have a `click` event. To make an icon clickable, use **Icon Button** or wrap the icon in a **Container** and wire the container's `click` event.

---

## Icon Libraries

Scram ships with icons from multiple libraries. The active library for a project is set in the theme. Available libraries:

| **Library** | **Style** |
| --- | --- |
| `feather` | Clean, minimal line icons |
| `hero-outline` | Outlined stroke icons (Heroicons) |
| `hero-solid` | Filled solid icons (Heroicons) |
| `lucide` | Refined line icons, Feather-derived |
| `material-outline` | Material Design outlined icons |
| `material-round` | Material Design rounded icons |
| `material-sharp` | Material Design sharp icons |
| `material-twotone` | Material Design two-tone icons |

Use icons from the library that matches your theme for visual consistency. Mixing libraries on the same page is possible but may look inconsistent.

---

## Accessibility

The **"Just a decorative Icon?"** toggle controls whether the icon is announced to screen readers.

| **Setting** | **Behaviour** |
| --- | --- |
| `false` *(default)* | The icon is treated as meaningful content and exposed to assistive technology. |
| `true` | The icon is hidden from assistive technology (`aria-hidden`). |

**Set `decorative: true` when:**

- The icon appears next to a text label that already conveys the same meaning (e.g. a search icon beside the word "Search").
- The icon is purely aesthetic — a decorative flourish or background element.

**Leave `decorative: false` when:**

- The icon is the only indicator of meaning (e.g. a standalone warning triangle with no accompanying text).

---

## Key Points

- **Icons cannot contain child components.** They are atomic — their only configurable content is the icon name and size.
- **Icons do not respond to `click`.** Use Icon Button for interactive icons, or place the icon inside a clickable Container.
- **Colour is set via the `color` style property**, not a dedicated prop. This means you can bind it to any expression — for example, changing colour based on a status: `status === 'error' ? theme.colors.error["500"] : theme.colors.success["500"]`.
- **Icons are `flex: none`**, so they never compress inside tight flex layouts. Their size is always exactly what `iconSize` specifies.
- **At `md` (24px)**, icons align naturally with `theme.text.md` body text when placed in a row container with `alignItems: center`.