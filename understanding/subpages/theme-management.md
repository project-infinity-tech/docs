---
title: "Theme Management"
description: "Defining and managing your app's visual theme in Scram."
---

Themes are Scram's way of controlling the visual style of your entire app from one place. Every component uses theme variables instead of hardcoded values — change a theme colour and every button, card, and heading updates at once.

Every project comes with a default theme. You can customise it or add new themes from the **Theme** option in the Top Navigation.

---

## What a theme controls

| Setting | Description |
|---|---|
| Colours | Named colour roles, each with automatically generated shades |
| Typography | Heading and body fonts |
| Spacing | How much breathing room components have |
| Text size | The base size scale for all text |
| Roundness | How curved corners are |
| Border weight | How thick borders appear |

---

## Colour roles

Rather than picking individual colours for every component, you assign colours to **roles** — each role has a purpose and Scram applies it consistently across your app.

| Role | Used for |
|---|---|
| Primary | Buttons, links, key actions |
| Secondary | Supporting accents |
| Surface | Backgrounds, cards, panels |
| Neutral | Borders, icons, muted text |
| Content | Body text and headings |
| Success / Alert / Error | Status indicators |

Pick one hex colour per role and Scram automatically generates 11 shades — from very light to very dark — for you to use across the design.

---

## Applying themes

Themes can be applied at three levels:

- **App** — one theme for the whole app (the default)
- **Page** — override the theme on a specific page
- **Component** — override the theme on an individual component

This lets you do things like give an admin section a different colour scheme without affecting the rest of the app.

---

## The theme editor tabs

**Set** — define the broad visual direction: colour scheme (Light, Dark, or Both), colour roles, fonts, and appearance scales.

**Refine** — fine-tune the underlying theme variables directly. This is where you set the exact pixel values for spacing, text sizes, border widths, and roundness — defining each scale value once so it applies consistently everywhere.

**Apply** — not yet live.