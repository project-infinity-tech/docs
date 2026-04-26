# Styled Container

## Overview

**Styled Container** is a pre-themed content panel that groups related content within a page. Where a plain Container is a blank, invisible box, a Styled Container arrives with surface colour, rounded corners, padding, and overflow clipping already applied — giving content an immediate sense of being contained and elevated from the background.

It renders as an HTML `<section>` element, making it the semantically correct choice for distinct regions of page content.

---

## Slots

| **Slot** | **Description** |
| --- | --- |
| **default** | Place any content here — headings, text, form inputs, images, or other components. |

---

## Properties

| **Property** | **Type** | **Default** | **Description** |
| --- | --- | --- | --- |
| **Section Title if No Heading in Content** (`title`) | Text | *(unset)* | If the content inside does not include a heading (`h2`–`h6`), provide one here to preserve semantic accessibility. Screen readers use headings to navigate sections. |

---

## Default Styles

Styled Container ships with a complete set of pre-applied theme-aware styles:

| **Property** | **Default** | **Notes** |
| --- | --- | --- |
| `background` | `neutral[50]` | A very light off-white, lifting the panel above a white page background. |
| `borderRadius` | `theme.roundness.md` | Rounded corners following the active theme. |
| `padding` | `theme.spacing.lg` | Generous internal spacing. |
| `width` | `100%` | Fills the width of its parent by default. |
| `display` | `flex` |  |
| `flexDirection` | `column` | Children stack vertically. |
| `rowGap` / `columnGap` | `theme.spacing.sm` | Consistent gap between child components. |
| `overflow` | `hidden` | Content is clipped to the rounded corners. |
| `borderStyle` | `none` | No border by default. |

All of these can be overridden in the styles panel.

---

## Events

| **Event** | **Fires when…** |
| --- | --- |
| `click` | User clicks anywhere inside the panel |
| `doubleClick` | User double-clicks |
| `mouseEnter` | Pointer enters the panel |
| `mouseLeave` | Pointer leaves the panel |
| `contextMenu` | User right-clicks |
| `blur` | Panel loses focus |

---

## Styled Container vs Container

|  | **Container** | **Styled Container** |
| --- | --- | --- |
| **HTML element** | `div` | `section` |
| **Background** | Transparent | `neutral[50]` |
| **Border radius** | None | `theme.roundness.md` |
| **Padding** | None | `theme.spacing.lg` |
| **Overflow** | Visible | Hidden |
| **Gap between children** | None | `theme.spacing.sm` |
| **Semantic meaning** | Generic grouping | Distinct content section |

Use **Container** when you need a neutral, invisible layout wrapper. Use **Styled Container** when you want a visually distinct panel that signals "this content belongs together" — dashboard widgets, settings sections, form panels, and detail cards are all good candidates.

---

## Accessibility

Because Styled Container renders as a `<section>`, it creates a landmark region in the accessibility tree. Screen reader users can navigate directly to it. For this reason, **every Styled Container should contain a heading** (`h2`–`h6`). If your content doesn't include one, use the `title` property to provide one — it will be added semantically even if it isn't visually prominent.

---

## Key Points

- **The surface colour is `neutral[50]`**, not white. On a white page this creates a subtle but clear visual separation. If your page background is already `neutral[50]`, increase the panel's background to `neutral[100]` to maintain the contrast.
- **`overflow: hidden` clips to rounded corners.** This is intentional — it ensures images and coloured child elements don't bleed outside the panel's rounded edges. If you need content to visually escape the panel (e.g. a floating badge), override `overflow` to `visible`.
- **Width is `100%` by default.** Inside a flex row layout, panels will share width equally. Set a specific width or `maxWidth` if you need panels of different sizes.
- **It is the surface used by Overlay Container internally.** The dialog panel inside Full Screen Overlay is a Styled Container.