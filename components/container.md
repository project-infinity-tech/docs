# Container

## Overview

**Container** is the fundamental building block of every layout in Scram. It is a general-purpose `div` that holds other components and controls their arrangement. Almost every page and component is built by nesting containers inside containers, each one responsible for the layout of its own children.

If you have used CSS flexbox before, the Container is essentially a `display: flex` div with every flexbox property exposed as a style setting.

---

## Slots

| **Slot** | **Description** |
| --- | --- |
| **default** | Place any components here. The container arranges them according to its layout styles. |

---

## Default Layout Behaviour

Out of the box, a Container stacks its children **vertically** (`flexDirection: column`). This is the most common layout needed for building top-to-bottom page sections. Switch `flexDirection` to `row` to arrange children side by side.

---

## Style Properties

Containers expose the full range of layout, spacing, visual, and positioning styles.

### Flexbox Layout

| **Property** | **Default** | **Description** |
| --- | --- | --- |
| `display` | `flex` | Always flex. |
| `flexDirection` | `column` | `column` stacks children vertically; `row` places them side by side. |
| `flexWrap` | `nowrap` | Whether children wrap to a new line when they run out of space. |
| `justifyContent` | `start` | Alignment along the main axis (the direction set by `flexDirection`). |
| `alignItems` | `start` | Alignment along the cross axis (perpendicular to `flexDirection`). |
| `rowGap` | `0px` | Vertical space between children. |
| `columnGap` | `0px` | Horizontal space between children. |

> ***Alignment values:** Use `start`, `center`, `end`, `space-between`, `space-around`, and `space-evenly`. Do not use `flex-start` or `flex-end` — these are not supported.*
> 

### Sizing

| **Property** | **Default** |
| --- | --- |
| `width` | `auto` |
| `minWidth` | `auto` |
| `maxWidth` | `auto` |
| `height` | `auto` |
| `minHeight` | `auto` |
| `maxHeight` | `auto` |
| `aspectRatio` | `auto` |

### Spacing

| **Property** | **Default** |
| --- | --- |
| `padding` | `0` |
| `margin` | `auto` |

### Visual

| **Property** | **Default** |
| --- | --- |
| `background` | `transparent` |
| `borderRadius` | `0` |
| `borderWidth` | `medium` |
| `borderColor` | `currentcolor` |
| `borderStyle` | `none` |
| `boxShadow` | `none` |
| `opacity` | `1` |
| `color` | `canvastext` |
| `overflow` | `visible` |

> ***Border shorthand warning:** Never set `border` as a single shorthand. Always set `borderWidth`, `borderStyle`, and `borderColor` as separate properties. Using the shorthand breaks the styling system.*
> 

### Positioning

| **Property** | **Default** |
| --- | --- |
| `position` | `static` |
| `top` / `right` / `bottom` / `left` | *(unset)* |
| `zIndex` | `auto` |

### Interaction

| **Property** | **Default** | **Description** |
| --- | --- | --- |
| `cursor` | `auto` | Pointer shape on hover. |
| `pointerEvents` | `auto` | Set to `none` to make the container click-through. |
| `userSelect` | `auto` | Whether text inside can be selected. |

---

## Properties

| **Property** | **Type** | **Default** | **Description** |
| --- | --- | --- | --- |
| **Tab Navigation** (`tabIndex`) | Enum | `default` | Controls whether the container participates in keyboard tab navigation. |

### Tab Navigation Options

| **Value** | **Behaviour** |
| --- | --- |
| `default` | Not in the tab order. Standard div behaviour. |
| `focusable` | Added to the tab order. Users can tab onto it, but it is not focused automatically on page load. |
| `autofocus` | Added to the tab order and focused immediately when the page loads. |

---

## Events

| **Event** | **Fires when…** |
| --- | --- |
| `click` | User clicks anywhere inside the container |
| `doubleClick` | User double-clicks the container |
| `mouseEnter` | Pointer enters the container |
| `mouseLeave` | Pointer leaves the container |
| `focus` | Container receives keyboard focus |
| `blur` | Container loses keyboard focus |
| `keyDown` | A key is pressed while the container is focused. The key pressed is available via `trigger.payload`. |

---

## Key Points

- **Everything is a Container.** Page sections, card wrappers, form layouts, grid cells — all of these are Containers with different style configurations.
- **Children do not inherit styles.** Setting `color` or `fontSize` on a Container does not cascade to its children. Apply text styles directly to the text components inside.
- **Responsive styles are additive.** Set your desktop styles first, then override specific properties at tablet and mobile breakpoints. Properties you don't override keep their desktop value.
- **Use `rowGap` and `columnGap` for spacing between children**, not margins on individual children. This keeps spacing consistent and easier to adjust.
- **`flexDirection: row` with `flexWrap: wrap`** is the standard pattern for responsive multi-column layouts that collapse to a single column on mobile.