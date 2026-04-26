# Breadcrumb Item

## Overview

**Breadcrumb Item** is the individual `<li>` element inside a Breadcrumb. It renders in one of two visual states depending on whether an `href` is provided, and optionally shows a separator icon after itself.

It is used automatically inside Breadcrumb via a Repeater and rarely needs to be placed manually. However it is available as a standalone component for custom breadcrumb layouts.

---

## Visual States

| **State** | **Condition** | **Appearance** |
| --- | --- | --- |
| **Link** | `href` is set | `neutral[500]` text, underlines on hover |
| **Current page** | `href` is empty / not set | `neutral[950]` text, `fontWeight: 500`, no underline |
| **With separator** | `showSeparator: true` | ChevronRight icon (or custom) after the label |
| **Without separator** | `showSeparator: false` | No icon — used for the last item |

Both the link and the current-page label are present in the DOM simultaneously; which one is visible is controlled by whether `href` is set. Font size for both is `theme.text.sm`.

---

## Properties

| **Property** | **Type** | **Default** | **Description** |
| --- | --- | --- | --- |
| **Label** (`label`) | Text | *(unset)* | Display text for this crumb |
| **URL** (`href`) | Text (URL) | *(unset)* | Destination URL or path. Leave empty to render as the current page (no link). |
| **Show Separator** (`showSeparator`) | Boolean | `true` | Whether to render the separator icon after this item. Set to `false` on the last item. |
| **Separator Icon** (`separatorIcon`) | Icon name | `ChevronRight` | The icon used as the separator. Override to use a different separator such as `Slash` or `ChevronDoubleRight`. |

---

## Events

Breadcrumb Item has no events.

---

## Key Points

- **The last crumb should always have no `href`** — this identifies it as the current page and renders it in darker, non-linked text. The Breadcrumb component sets `showSeparator: false` on the last item automatically.
- **Separators are part of each item**, not a separate component between items. The last item has its separator hidden via `showSeparator: false`.
- **The separator icon defaults to `ChevronRight`**. Change it via the `separatorIcon` property — the same icon is used for every separator in the trail, so for consistency set it on the Breadcrumb level rather than per item.
- **`href` accepts plain URL strings** — `/products/laptops`, `https://example.com`, or a dynamic expression. It does not accept the Link object format used by the Link component.
- **Dynamic breadcrumbs**: Bind `crumbs` to a computed array expression or page variable to generate the trail from the current route context, e.g. built from `page.pathParams`.