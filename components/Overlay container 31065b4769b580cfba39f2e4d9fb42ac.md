# Overlay container

## Overview

**Overlay Container** is a positioned card panel that floats above its surrounding content. It provides the white dialog surface you see inside a **Full Screen Overlay**, but it is also available as a standalone component for situations where you need content to appear above its parent — without covering the entire viewport.

Think of it as "a card that layers on top of things" rather than a full-screen takeover.

---

## Structure

```
┌─ parent context ──────────────────────────────┐
│                                               │
│   ┌─ Overlay Container (z-index: 5) ────────┐ │
│   │                                         │ │
│   │   default slot                          │ │
│   │   (your content)                        │ │
│   │                                         │ │
│   └─────────────────────────────────────────┘ │
│                                               │
└───────────────────────────────────────────────┘
```

Internally it renders as a `pla_contentcard` — a card-surfaced container — set to `position: relative` and `z-index: 5`, stacking it above normally-positioned siblings.

---

## Slots

| **Slot** | **Description** |
| --- | --- |
| **default** | Place any content here. The panel stacks it vertically with a small gap between items. |

---

## Style Properties

| **Property** | **Default** |
| --- | --- |
| `width` | `auto` |
| `minWidth` | `auto` |
| `maxWidth` | `auto` |
| `height` | `auto` |
| `minHeight` | `auto` |
| `maxHeight` | `auto` |
| `aspectRatio` | `auto` |
| `padding` | `0` |
| `margin` | `auto` |
| `position` | `relative` |

---

## Events

| **Event** | **Fires when…** |
| --- | --- |
| `click` | User clicks the panel |
| `doubleClick` | User double-clicks the panel |
| `contextMenu` | User right-clicks the panel |
| `mouseEnter` | Pointer enters the panel |
| `mouseLeave` | Pointer leaves the panel |
| `blur` | Panel loses focus |

---

## Relationship to Full Screen Overlay

Overlay Container is **embedded inside Full Screen Overlay** as its dialog panel. In most cases you will interact with it indirectly — you design content into the Full Screen Overlay's Dialog Slot, which places it inside this component automatically.

| **Component** | **Role** |
| --- | --- |
| **Full Screen Overlay** | Manages the backdrop, viewport coverage, open/close state |
| **Overlay Container** | Provides the white card surface that the dialog content sits on |

Use Overlay Container **standalone** when you want a floating panel anchored to a specific part of the page — for example, a dropdown panel, an inline tooltip card, or a context menu — rather than a full modal that covers everything.

---

## Key Points

- **It is a card, not just a div.** The panel has the same surface styling as `pla_contentcard` — background, shadow, and border radius from the theme. You do not need to add a card wrapper around it.
- **`z-index: 5` is baked in.** This is sufficient to clear most normal content. If you need it to clear components with higher `z-index` values, wrap it in a container and set a higher `z-index` on the wrapper.
- **`position: relative`** means it occupies space in the normal document flow. It does not float freely like a `position: absolute` or `position: fixed` element unless you override `position` in its styles.
- **Inner layout is `flexDirection: column`** with `theme.spacing.sm` gaps between children. Place a Container inside if you need a different inner layout direction.