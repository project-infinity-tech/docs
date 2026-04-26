# Link

## Overview

**Link** is a navigation wrapper — it has no visual style of its own. Instead, it wraps any other components (text, images, cards, avatars, containers) and makes the entire wrapped area a single clickable link that navigates to another page or URL.

The Link handles all routing, accessibility, keyboard navigation, and focus behaviour. Your slotted content handles all the visual design.

> ***Use Link when clicking should navigate.** For triggering actions, toggling state, or running workflows, use a button with a NavigateToPath step instead.*
> 

---

## Slots

| **Slot** | **Description** |
| --- | --- |
| **default** | Any component(s) placed here become the clickable link area. The entire slot content is wrapped in a single `<a>` element. |

---

## Properties

| **Property** | **Type** | **Description** |
| --- | --- | --- |
| **Link** (`link`) | Link object | The navigation destination. Configure the target page, path parameters, query parameters, and whether to open in a new tab. |

### The Link Object

The `link` property is a structured object with four fields:

| **Field** | **Description** |
| --- | --- |
| `identifier` | The destination. Either a reference to an internal page (`pages.pageId`) or an external URL string (`"https://example.com"`). |
| `target` | Where to open the link. Omit for same tab; set to `"_blank"` to open in a new tab. |
| `pathParams` | An object of dynamic path segment values for pages with path parameters (e.g. `{ id: current.data.userId }`). |
| `queryParams` | An object of query string values (e.g. `{ tab: "settings" }`). |

### Link Object Examples

**Internal page:**

```
{ identifier: pages.productDetail }
```

**Internal page with path parameter:**

```
{ identifier: pages.productDetail, pathParams: { id: current.data.productId } }
```

**Internal page with query parameters:**

```
{ identifier: pages.search, queryParams: { q: vars.searchTerm } }
```

**External URL, new tab:**

```
{ identifier: "https://example.com", target: "_blank" }
```

---

## Style Properties

| **Property** | **Default** |
| --- | --- |
| `color` | `primary[600]` |
| `fontFamily` | `sans-serif` |
| `fontWeight` | `500` |
| `fontSize` | `medium` |
| `lineHeight` | `normal` |
| `textAlign` | `left` |
| `background` | `transparent` |
| `opacity` | `1` |
| `borderStyle` | `none` |
| `boxShadow` | `none` |
| `padding` | `0` |
| `margin` | `auto` |
| `width` / `height` | `auto` |

The default `color: primary[600]` only affects inline text that inherits colour from the link element. When wrapping non-text content (images, cards, containers), this colour has no visible effect — the slotted content renders with its own styles.

The link renders as `display: inline-flex` by default.

---

## Events

Link has **no events**. Navigation happens automatically when clicked — no workflow is required.

---

## Link vs Button with NavigateToPath

|  | **Link (`pla_link`)** | **Button + NavigateToPath** |
| --- | --- | --- |
| **Visual** | None — inherits from slot content | Button appearance |
| **Interaction** | Click navigates immediately | Click triggers a workflow step |
| **Right-click / open in new tab** | ✅ Works natively (it's an `<a>` tag) | ❌ Not supported |
| **Keyboard navigation** | ✅ Full `<a>` semantics | Varies |
| **Pre-navigation logic** | ❌ Not possible | ✅ Run any steps first |
| **Use for** | Images, cards, text, avatars | Buttons, conditional navigation |

Use **Link** for anything that should behave like a hyperlink. Use a **Button + NavigateToPath** when you need to run logic (check permissions, save data, validate a form) before navigating.

---

## Common Patterns

### Clickable card

```
Link (link → pages.productDetail, pathParams: { id: current.data.id })
└── Card
    └── product content
```

### Clickable image

```
Link (link → pages.articleDetail, pathParams: { slug: current.data.slug })
└── Image (imgSrc = current.data.thumbnail)
```

### Inline text link

```
<p>Read our <Link link={{ identifier: pages.privacyPolicy }}>privacy policy</Link>.</p>
```

*(Note: In Scram, place the Link alongside a Text component in a flex container rather than nesting inside a Text component, as text components cannot have child components.)*

### External link in a new tab

```
Link (link → { identifier: "https://docs.example.com", target: "_blank" })
└── "View documentation →"
```

---

## Key Points

- **Link adds no visual chrome.** Border, underline, hover colour — all of these must come from the slotted content or from Link's own style overrides.
- **The entire slot is one link.** Every component inside the default slot is part of the same clickable region. To have two different link destinations inside a card, use two separate Link components inside the card.
- **Path parameters must match the target page's route.** If a page has a `:id` segment, you must pass `pathParams: { id: value }` or navigation will fail.
- **Right-click and middle-click work** because Link renders a real `<a>` element — users can open it in a new tab from the context menu, which is not possible with a Button workflow.
- **Do not nest Links.** Placing a Link inside another Link produces invalid HTML and unpredictable navigation behaviour.