---
title: "Understanding Themes"
---

A theme is the visual foundation of your app. It defines the colours, typography, spacing, and shape that every component inherits. Rather than styling each component individually, you set your design intentions once in a theme, and the entire app reflects them consistently.

---

## What a Theme Controls

A theme has four main concerns:

**Colour** — A palette of semantic colour roles that map to specific purposes in your UI. Not just "blue" and "grey", but *what those colours mean*.

**Typography** — The fonts used for headings and body text across the app.

**Spacing** — How much room exists between and around elements. Controls padding, margins, and gaps throughout the component library.

**Shape** — How rounded or sharp the corners are. A high roundness value gives a soft, modern feel; a low value gives a crisp, utilitarian one. Border width follows the same principle.

Text size is also controlled globally — the scale at which all type is rendered relative to the base.

---

## The Colour System

Scram's colour system is built around **semantic roles** rather than raw colours. Each role has a name that describes its *purpose*, not its appearance.

| **Role** | **Purpose** |
| --- | --- |
| **Primary** | Brand colour. Main CTAs, navigation highlights, key interactive elements. |
| **Secondary** | Supporting accent. Secondary actions, complementary highlights. |
| **Surface** | Background colour of the app, cards, panels, and modals. |
| **Neutral** | Borders, dividers, icons, disabled states, field backgrounds, and muted text. |
| **Content** | Body text, headings, and readable content. |
| **Success** | Positive feedback — confirmations, completed states, green indicators. |
| **Alert** | Warnings and caution states. |
| **Error** | Errors, validation failures, and destructive actions. |

Each role is more than a single colour. When you set a role to a hex value, Scram automatically generates an **11-shade scale** from that colour, ranging from very light (shade `50`) to very dark (shade `950`), with your chosen colour anchored at shade `500`.

This scale defines components' hover states, backgrounds, borders, and text colours, so you don't need to define each one. A button's hover state, a chip's background, an alert's border — all derived automatically from the right shade of the right role.

---

## Shades in Practice

When you reference a theme colour in a component or expression, you specify both the role and the shade:

`theme.colors.primary["500"]` — the primary colour itself

`theme.colors.primary["100"]` — a very light tint, useful for subtle background

`themes.colors.neutral["300"]` — a light grey, good for borders

`theme.colors.neutral["600"]` — a medium grey, good for secondary text

The lighter shades (50–200) work for backgrounds and tints. The middle shades (400–600) work for the colour itself and icons. The darker shades (700–950) work for text on light backgrounds and pressed states.

> ***Note on neutral:** Neutral is the most important colour to get right. It controls borders, dividers, field backgrounds, and muted icons throughout the UI. If you set neutral too light, these elements become invisible against a white surface. Always choose a medium-dark grey for neutral — darker than you think you need.*
> 

---

## Design Scales

Alongside colour, four numeric scales shape the proportions of your UI:

**Spacing** controls the layout's density — how much padding components have and how far apart elements sit. A lower value is compact; a higher value is airy. Values 3–4 produce a normal, comfortable layout.

**Text Size** scales all typography uniformly up or down. Values 3–4 produce standard, readable body text. Going higher produces noticeably large type; lower produces dense, compact text.

**Border** controls the width of borders throughout the UI. A value of 1 gives clean, subtle borders. Higher values make borders more pronounced.

**Roundness** controls the corner radius on buttons, cards, inputs, and other components. Lower values (2–3) give a sharp, flat aesthetic. Middle values (5–6) give a modern, rounded feel. Higher values produce very rounded, pill-like shapes.

The scales are not linear — values above 5 or 6 increase rapidly and can appear exaggerated. Treat 3–4 as "normal" for spacing and text size, and 5–6 as "normal" for roundness.

---

## Theme Hierarchy

Themes can be applied at three levels, each overriding the one above it:

**App level** — The default theme for the entire app. Every page and component inherits this unless overridden.

**Page level** — A different theme applied to a specific page. Useful for landing pages, login screens, or sections with a distinct visual identity.

**Component level** — A theme override on an individual component. Rarely needed, but available for cases where a single element needs to stand apart.

In practice, most apps use a single app-level theme and never override it. The hierarchy exists when you genuinely need visual variation between sections.

---

## Creating and Editing Themes

Themes are managed in the theme editor. You can create multiple themes and switch between them, or maintain separate themes for different contexts (e.g., light and dark).

When editing a theme, you set the base colour for each role (as a hex value) and Scram generates the full shade scale from it. You can then preview how components look with those colours before applying the theme to your app.

---

## Using Theme Values in Expressions

Theme values are available in expressions throughout the editor — in component styles, custom components, and anywhere CSS-like properties are set.

```
theme.colors.primary["500"]
theme.spacing.md
theme.roundness.lg
theme.border.sm
theme.font.body
theme.text.md
```

When you use theme variables instead of hardcoded values, your components automatically update if the theme changes — keeping the entire app visually consistent without manual rework.

---

## Key Things to Know

**Your colour choice becomes shade 500.** The auto-generated lighter shades are used throughout the UI for backgrounds and borders. If your chosen colour is already very light, those lighter shades will be nearly invisible. Anchor each role at a mid-to-dark value and let the scale do the work.

**Neutral carries the most weight.** More of your UI is rendered in neutral shades than in any other role. Getting neutral right — a medium-dark grey — has the biggest impact on the app's polish.

**Restraint with primary and secondary.** The temptation is to use your brand colour everywhere. A better approach is to reserve primary for key actions and interactive elements only. Most of the UI should read neutrally and in surface tones, with colour used to draw the eye where it matters.

---

## Related

- [Understanding Data Types →](Understanding%20Data%20Types%2030a65b4769b580c98459c222b812cfed.md)
- [Building Custom Component Definitions →](https://app.projectinfinity.tech/branch/cmmc094nh00q0p72m8f4d8ejn/fe/app/aAA_p111_00001/page/pAA_p111_00001/settings)
- [Working with Expressions →](Understanding%20Expressions%2015965b4769b580aab433dc5ea4a9f19d.md)