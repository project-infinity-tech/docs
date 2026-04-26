# Breadcrumbs

## Overview

**Breadcrumb** renders a horizontal trail of navigational links showing the user's current location within the page hierarchy. Each item except the last is a clickable link; the last item represents the current page and is displayed as plain text.

```
Home  ›  Products  ›  Laptops  ›  MacBook Pro 14"
  ↑           ↑           ↑              ↑
 link        link        link       current page
```

---

## Structure

The component renders as a semantic `<nav aria-label="breadcrumb">` containing an ordered list (`<ol>`). Items wrap to a new line on narrow screens using `flexWrap: wrap`.

---

## Properties

| **Property** | **Type** | **Description** |
| --- | --- | --- |
| **Breadcrumbs** (`crumbs`) | Array of objects | The full list of crumbs from root to current page. |

### Crumbs Item Structure

Each object in the `crumbs` array:

| **Field** | **Type** | **Description** |
| --- | --- | --- |
| `label` | Text | The display text for this crumb |
| `href` | URL / text | The URL or path this crumb links to. **Leave empty for the current page** — items without an `href` render as plain unlinked text. |

### Example

```
[
  { "label": "Home",     "href": "/" },
  { "label": "Products", "href": "/products" },
  { "label": "Laptops",  "href": "/products/laptops" },
  { "label": "MacBook Pro 14"" }
]
```

The last item has no `href` — it becomes the current page label, rendered in darker text with no underline.

---

## Events

Breadcrumb has no events.

---

## Accessibility

- Renders as `<nav aria-label="breadcrumb">` — screen readers announce it as a navigation landmark.
- Items are inside an `<ol>` (ordered list) — the sequence is semantically meaningful.
- No additional ARIA attributes are required.

[Breadcrumb Item](Breadcrumb%20Item%2031065b4769b5802ab247e7fc7a897b6b.md)