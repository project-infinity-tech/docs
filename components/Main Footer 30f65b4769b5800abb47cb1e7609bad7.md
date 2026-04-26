# Main Footer

## Overview

**Main Footer** is a structured, full-width footer with four independently fillable slots arranged across two rows. It ships with sensible dark defaults — a near-black background with light text — and handles its own responsive stacking on smaller screens. Like the navigation bar, it is pre-installed inside **Page Template Full** but can also be used standalone.

---

## Layout

The footer is divided into two rows separated by a horizontal divider:

```
┌─────────────────────────────────────────────────────────┐
│  [Leading]          [Content]              [Trailing]    │
│  Brand / logo       Nav link columns       Social icons  │
│                                            Newsletter    │
│─────────────────────────────────────────────────────────│
│  [Bottom]                                               │
│  Copyright notice, legal links, policies                │
└─────────────────────────────────────────────────────────┘
```

---

## Slots

| **Slot** | **Location** | **Typical Use** |
| --- | --- | --- |
| **Leading section** | Top-left | Logo, brand name, short tagline |
| **Content section** | Top-centre | Navigation link columns (Product, Company, Support, etc.) |
| **Trailing section** | Top-right | Social media icons, newsletter sign-up form |
| **Bottom section** | Below divider | Copyright notice, privacy policy, terms of service links |

The content section is given **twice the flex weight** (`flex: 2`) of the leading and trailing sections (`flex: 1` each), giving link columns more horizontal room.

---

## Properties

| **Property** | **Type** | **Default** | **Description** |
| --- | --- | --- | --- |
| **Background Color** (`backgroundColor`) | Text (colour expression) | `neutral[900]` | Fill colour of the entire footer. Accepts theme colour expressions or hex values. |
| **Text Color** (`textColor`) | Text (colour expression) | `neutral[300]` | Default text colour inherited by content inside the footer. |
| **Container width** (`containerWidth`) | Text | `1200px` | Maximum width of the inner content area. When used inside *Page Template Full*, this is passed in from the template automatically. |

> ***Using theme colours:** The background and text colour properties accept theme expressions such as `theme.colors.neutral["900"]` rather than plain hex values. This means the footer automatically adapts if you change your app's theme.*
> 

---

## Responsive Behaviour

| **Breakpoint** | **Top section** | **Bottom section** | **Padding** |
| --- | --- | --- | --- |
| **Desktop** | Three columns side by side | Row layout | `xl` vertical, `lg` horizontal |
| **Tablet** | Stacks vertically, columns separated by `lg` gap | Row layout | `lg` vertical, `md` horizontal |
| **Mobile** | Stacks vertically, columns separated by `md` gap | Stacks vertically, left-aligned | `md` vertical, `sm` horizontal |

---

## Style Properties

| **Property** | **Default** |
| --- | --- |
| `background` | `transparent` |

---

## Structure Detail

Internally the footer renders as:

1. **Footer Wrapper** — full-width column, carries the background colour, top border, and padding.
2. **Footer Content Container** — centred column capped at `containerWidth`, with `xl` gap between the top and bottom sections.
3. **Top Section** — three-slot row (leading, content, trailing).
4. **Divider** — a 1px horizontal rule in `neutral[800]`.
5. **Bottom Section** — a single slot row for legal content.

---

## Key Points

- The top border (`neutral[800]`) and internal divider are baked into the structure. If your design calls for no border, override the border width on the Footer Wrapper.
- The footer uses a **dark colour scheme by default** (`neutral[900]` background, `neutral[300]` text). If your design uses a light footer, update both `backgroundColor` and `textColor` accordingly — and remember that child components inherit the text colour set here.
- When used inside **Page Template Full**, `containerWidth` is passed in from the template. When used standalone, set it directly to match the rest of your layout.