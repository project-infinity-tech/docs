# Main Navigation

## Overview

**Main Navigation** is a responsive top navigation bar with three independently controllable zones: a leading section (typically your logo), a central content section (typically nav links), and a trailing section (typically user actions like a login button or avatar). It handles sticky positioning and collapses gracefully on mobile.

It is pre-installed inside the **Page Template Full**, but can also be placed on any page independently.

---

## Layout

The bar is divided into three horizontal zones that sit side by side:

```
┌────────────────────────────────────────────────────────┐
│  [Leading]        [Content]              [Trailing]     │
│  Logo, brand      Nav links             Login, avatar   │
└────────────────────────────────────────────────────────┘
```

All three zones stretch equally (`flex: 1`) so the content section is always perfectly centred, with leading and trailing sections anchored to their respective edges.

---

## Slots

| **Slot** | **Position** | **Typical Use** |
| --- | --- | --- |
| **Leading section** | Left | Logo, wordmark, brand link |
| **Content section** | Centre | Navigation links, search bar |
| **Trailing section** | Right | Login/signup buttons, user avatar, icons |

Drop any components into these slots — the navigation bar imposes no restrictions on what goes inside them.

---

## Properties

| **Property** | **Type** | **Default** | **Description** |
| --- | --- | --- | --- |
| **Sticky Navigation** (`sticky`) | Boolean | `true` | When on, the bar stays fixed to the top of the screen as the user scrolls. Turn off for a bar that scrolls away with the page. |
| **Background Color** (`backgroundColor`) | Colour | `#ffffff` | Fill colour of the bar. |
| **Border Color** (`borderColor`) | Colour | `neutral[200]` | Colour of the thin line along the bottom edge of the bar. |
| **Navigation Height** (`height`) | Text | `64px` | Height of the bar on desktop. On mobile the height is fixed at `56px` regardless of this setting. |
| **Container max width** (`containerWidth`) | Text | `1200px` | Maximum width of the inner content area. Content wider than this is centred and capped. When used inside *Page Template Full*, this value is passed in automatically from the template — you don't need to set it manually. |

---

## Responsive Behaviour

| **Breakpoint** | **Behaviour** |
| --- | --- |
| **Desktop** | All three sections visible. Height set by the `height` property. Horizontal padding uses `theme.spacing.lg`. |
| **Tablet** | All three sections visible. Padding reduces to `theme.spacing.md`. |
| **Mobile** | The **Content section is hidden** entirely. Height is fixed at `56px`. Padding reduces to `theme.spacing.sm`. |

> ***Mobile menus:** Because the content section disappears on mobile, if you have navigation links there you should also add a hamburger button to the trailing section that opens a mobile drawer or dropdown.*
> 

---

## Style Properties

| **Property** | **Default** |
| --- | --- |
| `maxWidth` | `auto` |
| `background` | `transparent` |

---

## Key Points

- The bar sits at `z-index: 1000`, so it always appears above page content when sticky.
- All three zones always render in the DOM — on mobile, the content section is hidden via `display: none`, not removed.
- When used inside **Page Template Full**, `containerWidth` is inherited from the template automatically. When using the navigation standalone, set it directly.
- The bottom border uses a `theme.border.sm` width, keeping it crisp and subtle across all themes.