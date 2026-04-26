# Card

### Overview

Card is a themed surface container for grouping related content. It provides a consistent elevated panel with rounded corners, a border, and a drop shadow — all driven by the theme. Its structure is divided into five optional sections: image, tag overlay, header, content, and footer, each toggled independently via props.

Use for: product cards, user profile summaries, article previews, dashboard widgets, list items inside a Repeater.

---

### Structure

```
┌──────────────────────────────┐
│  [Image]          [Tag] ──── │ ← absolute, top-right corner
│──────────────────────────────│
│  [Header slot]               │ ← showHeader
│ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─  │
│  [Content slot]              │ ← showContent (default: shown)
│ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─  │
│  [Footer slot]               │ ← showFooter
└──────────────────────────────┘
```

Dividers between Header/Content/Footer are rendered automatically and inherit the card theme colour.

---

### Slots

| **Slot** | **Description** |
| --- | --- |
| `Header` | Title, subtitle, avatar, action icons — anything at the top of the card body. |
| `Content` | The main body — descriptions, stats, form fields, data. Shown by default. |
| `Footer` | Actions, timestamps, metadata, buttons. Sits at the bottom. |

The image and tag are not slots — they are controlled via props (`imgSrc`, `tagLabel`).

---

### Properties

| **Property** | **Type** | **Default** | **Description** |
| --- | --- | --- | --- |
| `cardTheme` | enum | `neutral` | Semantic colour: `primary`, `secondary`, `neutral`, `error`, `alert`, `success`. Tints the border, background, and dividers. |
| `size` | enum | `sm` | `sm` / `md` / `lg` — scales internal padding and gaps across all sections. |
| `shadow` | enum | `sm` | `sm` / `md` / `lg` — controls drop shadow depth/elevation. |
| `showHeader` | boolean | `false` | Show or hide the Header section and its slot. |
| `showContent` | boolean | `true` | Show or hide the Content section and its slot. |
| `showFooter` | boolean | `false` | Show or hide the Footer section and its slot. |
| `showTag` | boolean | `false` | Show or hide the tag/badge overlay chip. |
| `imgSrc` | URL | — | Image URL displayed at the very top of the card, above the header. |
| `tagLabel` | text | — | Text for the tag/badge overlay (e.g. `"New"`, `"Featured"`, `"Sale"`). Only visible when `showTag` is `true`. |

---

### Style Properties

Key defaults (all theme-driven):

| **Property** | **Default** |
| --- | --- |
| `background` | `theme.colors[cardTheme]["50"]` |
| `borderColor` | `theme.colors[cardTheme]["100"]` |
| `borderWidth` | `theme.border.sm` |
| `borderRadius` | `theme.roundness.lg` |
| `boxShadow` | Varies by `shadow` prop: sm/md/lg preset values |
| `overflow` | `hidden` (clips image corners to match border-radius) |
| `flexDirection` | `column` |

---

### Events

**None.** The Card has no built-in click or interaction events. To make a card clickable, wrap it in a **Link** component (`pla_link`) or place a Button inside the Footer slot.

---

### Tag Overlay

When `showTag` is `true`, a **Chip** component is rendered absolutely positioned at the **top-right corner** of the card. Its theme matches `cardTheme` and its size matches the card `size`. The label text comes from `tagLabel`. This is suitable for short badges (1–2 words). For more complex badge styling, hide the tag and place a Chip manually inside the Header slot.

---

### Key Points

- Sections that are hidden (`showHeader: false` etc.) remain in the component tree — their slot content is preserved, just not visible
- **`overflow: hidden`** is set by default — this is what clips the top image to the card's rounded corners; be aware that absolutely positioned children outside the card bounds will also be clipped
- Dividers between sections are always rendered internally; they are only visible when the adjacent sections are shown
- The Card has **no events** and **no variables**
- The `cardTheme` colours are very light (`"50"` background, `"100"` border) — the card is designed to sit on a neutral surface, not to be a bold colour block
- To stack cards in a list or grid, place the Card inside a **Repeater**