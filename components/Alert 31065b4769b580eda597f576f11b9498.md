# Alert

## Overview

**Alert** is a full-width notification banner that communicates a status message to the user — a success confirmation, a warning, an error, or general information. It combines a leading icon, a text content area, an optional custom content slot, and an optional dismiss button into a single, semantically marked-up component.

---

## Structure

```
┌──────────────────────────────────────────────────────┐
│  🔔  Message text or custom slot content          ✕  │
└──────────────────────────────────────────────────────┘
  ↑          ↑                                      ↑
Leading   Content area                         Close button
 icon     (text + slot)                        (if closeable)
```

Renders as `<div role="alert">`, which causes screen readers to announce the content immediately when it appears.

---

## Properties

| **Property** | **Type** | **Default** | **Description** |
| --- | --- | --- | --- |
| **Theme** (`alertTheme`) | Enum | `neutral` | The semantic colour applied to the alert. Controls background, text, border, and icon colours automatically. |
| **Style** (`variant`) | Enum | `subtle` | The visual weight of the alert. |
| **Icon** (`alertIcon`) | Icon name | `AlertCircle` | The icon displayed at the left edge. Override to match the alert's meaning — e.g. `CheckCircle` for success, `XCircle` for error. |
| **Closeable** (`closeable`) | Boolean | `false` | When on, shows an ✕ button on the right. Wiring the `close` event to a workflow hides the alert when dismissed. |

---

### Theme Options

| **Value** | **Intended use** |
| --- | --- |
| `neutral` | General information, default messages |
| `primary` | Brand-coloured notices, feature announcements |
| `secondary` | Supporting notices |
| `success` | Confirmation, completion, saved state |
| `alert` | Warnings, caution notices |
| `error` | Failures, validation errors, destructive outcomes |

---

### Variant Options

| **Value** | **Background** | **Border** | **Text** |
| --- | --- | --- | --- |
| `subtle` | `theme[100]` (lightly tinted) | Transparent | `theme[700]` *(default)* |
| `solid` | `theme[500]` (fully filled) | Transparent | White (or `neutral[950]` for neutral theme) |
| `outline` | Transparent | `theme[500]` | `theme[600]` |

---

## Slots

| **Slot** | **Description** |
| --- | --- |
| **default** | Optional content placed alongside or after the text. Use for action links, buttons, or additional detail. |

The default slot sits inside the content row, after the main text span.

---

## Events

| **Event** | **Fires when…** |
| --- | --- |
| `onClick` | User clicks anywhere on the alert body |
| `close` | User clicks the ✕ dismiss button (only fires when `closeable` is `true`) |

### Dismissing an Alert

Wire the `close` event to hide the alert. The standard pattern:

1. Wrap the Alert in a Container or control its `scram-visible` with a page variable.
2. On the `close` event, set the page variable to `false`: 
`close → SetVariable vars.showAlert = false`
3. Bind `scram-visible` on the alert (or its wrapper) to `vars.showAlert`.

---

## Colour Logic Summary

All three visual elements — background, text, and icon — automatically coordinate their colours based on `alertTheme` and `variant`:

| **Variant** | **Background** | **Text / Icon** |
| --- | --- | --- |
| `subtle` | `theme[100]` | `theme[700]` |
| `solid` | `theme[500]` | `neutral[50]` (white) — except neutral theme uses `neutral[950]` |
| `outline` | Transparent | `theme[600]` |

You do not need to set colours manually. Override them in the styles panel only when you need to depart from the semantic defaults.

---

## Style Properties

| **Property** | **Default** |
| --- | --- |
| `width` | `100%` |
| `padding` | `theme.spacing.xs` |
| `borderRadius` | `theme.roundness.md` |
| `borderStyle` | `solid` |
| `borderWidth` | `theme.border.sm` |
| `borderColor` | Driven by `variant` and `alertTheme` |
| `background` | Driven by `variant` and `alertTheme` |
| `color` | Driven by `variant` and `alertTheme` |
| `rowGap` / `columnGap` | `theme.spacing.xxs` |
| `boxShadow` | `none` |
| `margin` | `auto` |

---

## Common Patterns

### Inline form validation error

```
alertTheme: error
variant: subtle
alertIcon: XCircle
Closeable: false
Content text: "Please fix the errors below before submitting."
```

### Success confirmation after saving

```
alertTheme: success
variant: subtle
alertIcon: CheckCircle
Closeable: true
Content text: "Your changes have been saved."
scram-visible: { vars.showSuccessAlert }
close → SetVariable vars.showSuccessAlert = false
```

### Warning with an action link

```
alertTheme: alert
variant: outline
alertIcon: AlertTriangle
Content text: "Your subscription expires in 3 days."
default slot: Button "Renew now" → NavigateToPath billing page
```

---

## Key Points

- **`role="alert"` is baked in.** Content placed in the alert is announced by screen readers immediately when the component becomes visible — no extra ARIA needed.
- **The icon colour always matches the text colour.** Both are driven by the same theme/variant logic, so they stay in sync without manual overrides.
- **The close button only appears when `closeable: true`.** The ✕ button is always in the DOM but hidden; enabling `closeable` makes it visible.
- **Alert is always full width** (`width: 100%`). Constrain it by placing it inside a width-limited container.
- **No animation built in.** For fade-in/out effects when showing or hiding, apply CSS transitions on the wrapping container.