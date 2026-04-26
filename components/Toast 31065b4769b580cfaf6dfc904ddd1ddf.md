# Toast

## Overview

**Toast** is a small, non-blocking notification panel that appears anchored to the bottom-right of its containing area. It is used for brief, transient messages that confirm an action, report a status, or surface a non-critical alert — without interrupting the user's flow or requiring a response.

Unlike Alert — which sits inline in the page layout — Toast uses `position: sticky` and the native `popover="auto"` behaviour to float over content.

---

## Structure

```
                              ┌────────────────────────┐
                              │  🔔  Toast Heading      │
                              │      Toast content      │
                              └────────────────────────┘
                                            ↑
                               bottom-right of container
```

Internally, the Toast is a `<div popover="auto">` wrapping a Styled Container card. The card contains a row of: an icon, and a column of heading (`h4`) and body text (`p`).

---

## Content

Toast has two editable text areas:

| **Area** | **Type** | **Default** |
| --- | --- | --- |
| **Heading** | Inline text (`h4`) | `"Toast Heading"` |
| **Body** | Rich text block (`p`) | `"Toast content"` |

Set both directly in the component tree — click the Heading 4 or Text sub-component to edit the content, or bind them to dynamic expressions.

---

## Properties

Toast has **no configurable properties** beyond its two text content areas. There are no theme, variant, icon, or size controls. Customise the appearance by editing the sub-components directly in the component tree:

- **Icon** — select the Icon sub-component and change `iconName` and `color`
- **Heading** — select the Heading 4 sub-component and edit text or styles
- **Body text** — select the Text sub-component and edit text or styles
- **Card surface** — select the Content Container (Styled Container) to adjust background, border, and shadow

---

## Events

Toast has **no events**.

---

## Positioning

The outer wrapper is `position: sticky`, anchored to `bottom: theme.spacing.xxxs, right: theme.spacing.xxxs`. This means:

- It sticks to the bottom-right of its **nearest scrolling ancestor** (not necessarily the viewport).
- It only appears sticky when the page is long enough to scroll. On short pages it sits in document flow.
- It is `width: fit-content` — it shrinks to wrap its content.

> ***For a true fixed-position toast** that always appears in the bottom-right corner of the viewport regardless of scroll position, wrap the Toast in a Container and set the container to `position: fixed`, `bottom: theme.spacing.md`, `right: theme.spacing.md`, `zIndex: 9999`.*
> 

---

## Showing and Hiding

Toast has no built-in open/close state or timer. The standard approach is to control its visibility with a page variable:

1. **Create a page variable** — e.g. `showToast`, type: boolean, default: `false`.
2. **Bind `scram-visible`** on the Toast to `vars.showToast`.
3. **Show the toast** from a workflow after a successful action: 
`SetVariable vars.showToast = true`
4. **Auto-dismiss** using a Run Code step immediately after, with a timed delay: `javascript
// Run Code body (executes async, does not block the workflow)
await new Promise(resolve => setTimeout(resolve, 3000));`
Then follow with: 
`SetVariable vars.showToast = false`

> ***Note:** The Run Code timeout approach runs client-side and will not block subsequent workflow steps. Place the SetVariable to hide the toast at the end of the workflow or in a separate workflow triggered after the delay.*
> 

---

## Toast vs [Alert](Alert%2031065b4769b580eda597f576f11b9498.md)

|  | **Toast** | **Alert** |
| --- | --- | --- |
| **Position** | Floating, bottom-right | Inline in page flow |
| **Layout impact** | None (overlaps content) | Takes up layout space |
| **Dismissal** | Typically auto-dismisses | Manually closed or persistent |
| **Interaction required** | No | Optional (close button) |
| **Theme/variant options** | None built-in | Full theme + variant system |
| **Best for** | Brief confirmations ("Saved", "Copied") | Persistent warnings, errors, notices |

---

## Key Points

- **Toast has no built-in timer or auto-dismiss.** You must implement the show/hide logic and any timeout yourself using page variables and workflows.
- **Styling is done through sub-components**, not top-level properties. There are no `theme` or `variant` props — edit the Icon, Heading, Text, and card container directly.
- **`popover="auto"`** is set on the outer wrapper. This is a native browser popover attribute that allows the element to appear above other content and be dismissed by clicking outside. Its behaviour may vary across browsers.
- **For multiple simultaneous toasts**, create a Repeater bound to a page variable array of toast messages, and render a Toast inside it.
- **For a fixed viewport position**, wrap in a `position: fixed` Container — the Toast's own `position: sticky` is not sufficient to pin it to the viewport corner independently.