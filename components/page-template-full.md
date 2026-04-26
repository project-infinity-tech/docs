# Page Template Full

## Overview

**Page Template Full** is a ready-made full-page layout that gives every page in your app a consistent structure. Drop it onto a page and you immediately get a top navigation bar, a content area in the middle, and a footer at the bottom — all wired together and ready to use.

Think of it as the "shell" of a page. You provide the content; the template handles the frame around it.

---

## Structure

The template is made up of three stacked sections:

```
┌─────────────────────────────────┐
│         Main Navigation         │  ← fixed top bar (branding, links, actions)
├─────────────────────────────────┤
│                                 │
│         Content Slot            │  ← your page-specific content goes here
│                                 │
├─────────────────────────────────┤
│           Main Footer           │  ← site-wide links, copyright, etc.
└─────────────────────────────────┘
```

| **Section** | **Component** | **Role** |
| --- | --- | --- |
| **Main Navigation** | `pla_mainnavigation` | Top bar with logo, nav links, and global actions |
| **Content Area** | Default slot | Where you place your page-specific components |
| **Main Footer** | `pla_mainfooter` | Bottom bar with supplementary links and information |

The outer wrapper stretches to at least the full viewport height (`min-height: 100vh`), so even short pages won't leave an empty gap before the footer.

---

## Properties

| **Property** | **Type** | **Default** | **Description** |
| --- | --- | --- | --- |
| **Container Width** (`containerWidth`) | Text | `1200px` | Maximum width of both the nav bar and the content area. Keeps content from stretching too wide on large screens. |
| **default** (slot) | Slot | — | The content area. Place any components here and they appear between the header and footer. |

---

## How to Use It

1. **Add the template to your page.** Place a *Page Template Full* at the root of your page — it should be the outermost component, wrapping everything else.
2. **Drop your content into the default slot.** Any components you add as children automatically appear in the main content area between the navigation bar and the footer.
3. **Adjust the container width** if needed. The default `1200px` suits most layouts, but you can widen or narrow it for different designs (e.g. `960px` for a tighter layout, `100%` for full-bleed).
4. **Customise the navigation and footer** by editing the `pla_mainnavigation` and `pla_mainfooter` sub-components within the template — for example, adding your logo, nav links, and social media icons.

---

## Layout Behaviour

- The content slot sits inside a centred container that respects the `containerWidth` limit.
- The content area uses `flex: 1` to fill all available vertical space between the header and footer, preventing the footer from "floating up" on short pages.
- On smaller screens, the contained width scales down naturally; use the navigation and footer components' own responsive settings for mobile-specific adjustments.

---

## Typical Usage Pattern

```
Page Root
└── Page Template Full          ← add this first
    └── [default slot]
        ├── Hero Section
        ├── Feature Grid
        └── Call to Action
```

---

## Related Components

- **Main Navigation** (`pla_mainnavigation`) — the top bar embedded in this template
    - [Main Navigation](Main%20Navigation%2030f65b4769b580a9a92def4f7e369405.md)
- **Main Footer** (`pla_mainfooter`) — the bottom bar embedded in this template
    - [Main Footer](Main%20Footer%2030f65b4769b5800abb47cb1e7609bad7.md)
- **Logo** (`pla_logo`) — pre-placed inside the navigation bar
    -